# SUNNY ECOSYSTEM 싱글사인온(SSO) 구현 방안 보고서

**작성일**: 2025-12-06
**대상 시스템**: SUNNY ECOSYSTEM (HIPUS AI, HDH Fintech, ProActive Senior, Company Valuation 등)
**목적**: 통합 인증 시스템 구축을 통한 사용자 경험 개선 및 보안 강화

---

## 1. 개요

### 1.1 현재 상황
- 각 서비스(HIPUS AI, HDH Fintech, ProActive Senior 등)가 독립적으로 운영
- 사용자가 각 서비스마다 별도 로그인 필요
- 로그인 상태가 JavaScript 변수(`isLoggedIn`)로만 관리
- 세션 영속성 없음 (새로고침 시 로그인 상태 초기화)

### 1.2 SSO 도입 목적
1. **사용자 경험 개선**: 한 번의 로그인으로 모든 서비스 이용
2. **보안 강화**: 중앙 집중식 인증 관리
3. **개발 효율성**: 인증 로직 중복 제거
4. **통합 관리**: 사용자 계정 및 권한 통합 관리
5. **확장성**: 새로운 서비스 추가 시 인증 시스템 재사용

---

## 2. SSO 구현 방식 비교

### 2.1 방식 1: LocalStorage 기반 간단한 SSO

#### 개요
- 메인 페이지에서 로그인 시 토큰을 브라우저 localStorage에 저장
- 모든 서비스가 동일한 도메인 하에서 localStorage 공유
- 각 서비스에서 토큰 존재 여부로 로그인 상태 확인

#### 장점
✅ 구현이 매우 간단하고 빠름
✅ 별도의 서버 없이 프론트엔드만으로 구현 가능
✅ 즉시 적용 가능
✅ 페이지 새로고침 후에도 로그인 상태 유지

#### 단점
❌ 보안이 약함 (XSS 공격에 취약)
❌ 같은 도메인에서만 작동
❌ 토큰 검증 로직 없음
❌ 중앙 관리 어려움
❌ 프로덕션 환경에는 부적합

#### 구현 난이도
⭐ (매우 쉬움)

#### 구현 예시
```javascript
// 로그인 시
function handleLogin(username, password) {
    // 인증 후
    const userData = {
        username: username,
        loginTime: new Date().toISOString(),
        token: 'simple-token-' + Date.now()
    };
    localStorage.setItem('sunny_user', JSON.stringify(userData));
}

// 로그인 확인
function checkLogin() {
    const userData = localStorage.getItem('sunny_user');
    return userData !== null;
}

// 로그아웃
function handleLogout() {
    localStorage.removeItem('sunny_user');
}
```

#### 적용 시나리오
- 프로토타입/MVP 단계
- 내부 테스트 환경
- 빠른 데모가 필요한 경우

---

### 2.2 방식 2: JWT(JSON Web Token) 기반 SSO

#### 개요
- 중앙 인증 서버에서 JWT 토큰 발급
- 각 서비스에서 JWT 검증
- Refresh Token으로 토큰 갱신

#### 장점
✅ 업계 표준 방식
✅ 토큰 자체에 사용자 정보 포함 (Stateless)
✅ 서명 검증으로 위변조 방지
✅ 만료 시간 설정 가능
✅ 확장성 우수
✅ 다른 도메인 간에도 작동

#### 단점
❌ 백엔드 서버 필요
❌ 구현 복잡도 중간
❌ Refresh Token 관리 필요
❌ 토큰 무효화가 어려움 (블랙리스트 필요)

#### 구현 난이도
⭐⭐⭐ (중간)

#### 아키텍처
```
[사용자]
   ↓ 로그인 요청
[인증 서버]
   ↓ JWT 발급 (Access Token + Refresh Token)
[클라이언트]
   ↓ JWT를 헤더에 포함하여 API 요청
[각 서비스 API]
   ↓ JWT 검증
[리소스 제공]
```

#### JWT 구조
```
Header:
{
  "alg": "HS256",
  "typ": "JWT"
}

Payload:
{
  "sub": "user_id",
  "name": "홍길동",
  "email": "user@example.com",
  "role": "premium",
  "iat": 1638360000,
  "exp": 1638363600
}

Signature:
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret
)
```

#### 구현 예시 (Node.js + Express)

**인증 서버**:
```javascript
const jwt = require('jsonwebtoken');
const SECRET_KEY = 'your-secret-key-keep-it-safe';

// 로그인 엔드포인트
app.post('/api/auth/login', async (req, res) => {
    const { username, password } = req.body;

    // 사용자 인증 (DB 조회)
    const user = await authenticateUser(username, password);

    if (!user) {
        return res.status(401).json({ error: 'Invalid credentials' });
    }

    // Access Token 생성 (15분 유효)
    const accessToken = jwt.sign(
        {
            sub: user.id,
            username: user.username,
            email: user.email,
            role: user.role
        },
        SECRET_KEY,
        { expiresIn: '15m' }
    );

    // Refresh Token 생성 (7일 유효)
    const refreshToken = jwt.sign(
        { sub: user.id },
        SECRET_KEY,
        { expiresIn: '7d' }
    );

    // Refresh Token은 DB에 저장
    await saveRefreshToken(user.id, refreshToken);

    res.json({
        accessToken,
        refreshToken,
        user: {
            id: user.id,
            username: user.username,
            email: user.email,
            role: user.role
        }
    });
});

// 토큰 갱신 엔드포인트
app.post('/api/auth/refresh', async (req, res) => {
    const { refreshToken } = req.body;

    try {
        const decoded = jwt.verify(refreshToken, SECRET_KEY);
        const isValid = await validateRefreshToken(decoded.sub, refreshToken);

        if (!isValid) {
            return res.status(401).json({ error: 'Invalid refresh token' });
        }

        const user = await getUserById(decoded.sub);

        const newAccessToken = jwt.sign(
            {
                sub: user.id,
                username: user.username,
                email: user.email,
                role: user.role
            },
            SECRET_KEY,
            { expiresIn: '15m' }
        );

        res.json({ accessToken: newAccessToken });
    } catch (error) {
        res.status(401).json({ error: 'Token verification failed' });
    }
});
```

**클라이언트 (프론트엔드)**:
```javascript
// 로그인 함수
async function login(username, password) {
    const response = await fetch('/api/auth/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password })
    });

    const data = await response.json();

    // 토큰 저장 (httpOnly 쿠키가 더 안전하지만 여기서는 localStorage 사용)
    localStorage.setItem('accessToken', data.accessToken);
    localStorage.setItem('refreshToken', data.refreshToken);
    localStorage.setItem('user', JSON.stringify(data.user));

    return data;
}

// API 호출 시 토큰 포함
async function callAPI(endpoint) {
    const accessToken = localStorage.getItem('accessToken');

    const response = await fetch(endpoint, {
        headers: {
            'Authorization': `Bearer ${accessToken}`
        }
    });

    // 토큰 만료 시 갱신
    if (response.status === 401) {
        await refreshAccessToken();
        return callAPI(endpoint); // 재시도
    }

    return response.json();
}

// 토큰 갱신
async function refreshAccessToken() {
    const refreshToken = localStorage.getItem('refreshToken');

    const response = await fetch('/api/auth/refresh', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ refreshToken })
    });

    const data = await response.json();
    localStorage.setItem('accessToken', data.accessToken);
}

// 로그아웃
async function logout() {
    localStorage.removeItem('accessToken');
    localStorage.removeItem('refreshToken');
    localStorage.removeItem('user');

    // 서버에 로그아웃 알림 (Refresh Token 무효화)
    await fetch('/api/auth/logout', { method: 'POST' });
}
```

**서비스별 미들웨어**:
```javascript
// JWT 검증 미들웨어
function authenticateToken(req, res, next) {
    const authHeader = req.headers['authorization'];
    const token = authHeader && authHeader.split(' ')[1];

    if (!token) {
        return res.status(401).json({ error: 'Access token required' });
    }

    jwt.verify(token, SECRET_KEY, (err, user) => {
        if (err) {
            return res.status(403).json({ error: 'Invalid token' });
        }

        req.user = user;
        next();
    });
}

// 보호된 라우트
app.get('/api/hdh-fintech/dashboard', authenticateToken, (req, res) => {
    // req.user에 토큰의 payload 정보가 있음
    res.json({
        message: `Welcome ${req.user.username}`,
        data: getDashboardData(req.user.sub)
    });
});
```

#### 필요한 인프라
- Node.js 서버 (또는 다른 백엔드)
- 데이터베이스 (사용자 정보, Refresh Token 저장)
- HTTPS (토큰 전송 보안)

#### 적용 시나리오
- **프로덕션 환경**
- 여러 서비스 간 SSO 필요
- 모바일 앱 연동 필요
- API 보안이 중요한 경우

---

### 2.3 방식 3: OAuth 2.0 기반 SSO

#### 개요
- 표준 OAuth 2.0 프로토콜 사용
- Authorization Server에서 인증 및 권한 부여
- 외부 서비스(Google, GitHub 등)와도 연동 가능

#### 장점
✅ 업계 표준 프로토콜
✅ 보안이 매우 강력
✅ 외부 소셜 로그인 연동 가능
✅ 세밀한 권한 관리 (Scope)
✅ 엔터프라이즈급 솔루션
✅ 감사 로그 및 모니터링 용이

#### 단점
❌ 구현 복잡도 높음
❌ 별도 Authorization Server 필요
❌ 설정 및 관리 복잡
❌ 학습 곡선 높음
❌ 오버엔지니어링 가능성

#### 구현 난이도
⭐⭐⭐⭐⭐ (매우 어려움)

#### OAuth 2.0 Flow (Authorization Code Grant)
```
[사용자]
   ↓ (1) 로그인 버튼 클릭
[클라이언트 앱]
   ↓ (2) 인증 요청 (redirect to Authorization Server)
[Authorization Server]
   ↓ (3) 로그인 페이지 표시
[사용자 로그인]
   ↓ (4) 인증 성공
[Authorization Server]
   ↓ (5) Authorization Code 발급 (redirect to Client)
[클라이언트 앱]
   ↓ (6) Authorization Code로 토큰 요청
[Authorization Server]
   ↓ (7) Access Token + Refresh Token 발급
[클라이언트 앱]
   ↓ (8) Access Token으로 API 호출
[Resource Server]
   ↓ (9) 리소스 제공
```

#### 구현 예시 (Keycloak 사용)

**1. Keycloak 설정**:
```yaml
# docker-compose.yml
version: '3'
services:
  keycloak:
    image: quay.io/keycloak/keycloak:latest
    environment:
      KEYCLOAK_ADMIN: admin
      KEYCLOAK_ADMIN_PASSWORD: admin
    ports:
      - 8080:8080
    command: start-dev
```

**2. 클라이언트 설정**:
- Realm: sunny-ecosystem
- Client ID: sunny-main-app
- Valid Redirect URIs: https://sunny-ecosystem.com/*
- Web Origins: https://sunny-ecosystem.com

**3. 프론트엔드 구현 (Keycloak JS Adapter)**:
```javascript
// Keycloak 초기화
const keycloak = new Keycloak({
    url: 'http://localhost:8080',
    realm: 'sunny-ecosystem',
    clientId: 'sunny-main-app'
});

// 초기화 및 자동 로그인 체크
keycloak.init({
    onLoad: 'check-sso',
    checkLoginIframe: true,
    pkceMethod: 'S256'
}).then(authenticated => {
    if (authenticated) {
        console.log('User is authenticated');
        loadUserProfile();
    } else {
        console.log('User is not authenticated');
    }
});

// 로그인
function login() {
    keycloak.login();
}

// 로그아웃
function logout() {
    keycloak.logout();
}

// 사용자 정보 가져오기
async function loadUserProfile() {
    const profile = await keycloak.loadUserProfile();
    console.log('User profile:', profile);
}

// API 호출 시 토큰 자동 포함
async function callProtectedAPI(endpoint) {
    await keycloak.updateToken(30); // 30초 이내 만료 시 갱신

    const response = await fetch(endpoint, {
        headers: {
            'Authorization': `Bearer ${keycloak.token}`
        }
    });

    return response.json();
}

// 토큰 갱신 이벤트
keycloak.onTokenExpired = () => {
    keycloak.updateToken(30).then(refreshed => {
        if (refreshed) {
            console.log('Token refreshed');
        }
    });
};
```

**4. 백엔드 검증 (Node.js)**:
```javascript
const KeycloakConnect = require('keycloak-connect');
const session = require('express-session');

const app = express();

// 세션 설정
const memoryStore = new session.MemoryStore();
app.use(session({
    secret: 'some-secret',
    resave: false,
    saveUninitialized: true,
    store: memoryStore
}));

// Keycloak 설정
const keycloak = new KeycloakConnect({ store: memoryStore }, {
    realm: 'sunny-ecosystem',
    'auth-server-url': 'http://localhost:8080',
    'ssl-required': 'external',
    resource: 'sunny-backend',
    'confidential-port': 0
});

app.use(keycloak.middleware());

// 보호된 라우트
app.get('/api/protected', keycloak.protect(), (req, res) => {
    res.json({
        message: 'Protected resource',
        user: req.kauth.grant.access_token.content
    });
});

// 역할 기반 접근 제어
app.get('/api/admin', keycloak.protect('realm:admin'), (req, res) => {
    res.json({ message: 'Admin only resource' });
});
```

#### 필요한 인프라
- Authorization Server (Keycloak, Auth0, Okta 등)
- 데이터베이스
- HTTPS 필수
- 도메인 및 SSL 인증서

#### 적용 시나리오
- **대규모 엔터프라이즈 환경**
- 다양한 외부 서비스 연동 필요
- 세밀한 권한 관리 필요
- 규정 준수(GDPR, HIPAA 등) 필요
- 수백 개 이상의 마이크로서비스

---

### 2.4 방식 4: Session 기반 SSO (Same Domain)

#### 개요
- 서버 세션을 사용한 전통적인 방식
- 쿠키를 통한 세션 ID 공유
- 같은 최상위 도메인에서만 작동

#### 장점
✅ 구현이 비교적 간단
✅ 서버에서 세션 제어 가능 (즉시 무효화)
✅ XSS 공격에 강함 (httpOnly 쿠키)
✅ 브라우저 기본 기능 활용

#### 단점
❌ 서버 메모리/스토리지 사용
❌ 수평 확장 시 세션 공유 복잡
❌ 같은 도메인에서만 작동
❌ 모바일 앱 지원 어려움
❌ Stateful (서버 부하)

#### 구현 난이도
⭐⭐ (쉬움)

#### 구현 예시
```javascript
// Express + express-session
const session = require('express-session');
const RedisStore = require('connect-redis')(session);
const redis = require('redis');

const redisClient = redis.createClient();

app.use(session({
    store: new RedisStore({ client: redisClient }),
    secret: 'session-secret',
    resave: false,
    saveUninitialized: false,
    cookie: {
        secure: true, // HTTPS only
        httpOnly: true, // JavaScript 접근 불가
        maxAge: 1000 * 60 * 60 * 24 * 7, // 7일
        domain: '.sunny-ecosystem.com', // 모든 서브도메인에서 공유
        sameSite: 'lax'
    }
}));

// 로그인
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = await authenticateUser(username, password);

    if (user) {
        req.session.userId = user.id;
        req.session.username = user.username;
        req.session.role = user.role;

        res.json({ success: true, user });
    } else {
        res.status(401).json({ error: 'Invalid credentials' });
    }
});

// 인증 미들웨어
function requireAuth(req, res, next) {
    if (req.session.userId) {
        next();
    } else {
        res.status(401).json({ error: 'Not authenticated' });
    }
}

// 보호된 라우트
app.get('/api/dashboard', requireAuth, (req, res) => {
    res.json({
        userId: req.session.userId,
        username: req.session.username
    });
});

// 로그아웃
app.post('/logout', (req, res) => {
    req.session.destroy(err => {
        if (err) {
            return res.status(500).json({ error: 'Logout failed' });
        }
        res.clearCookie('connect.sid');
        res.json({ success: true });
    });
});
```

#### 적용 시나리오
- 모든 서비스가 같은 도메인 하에 있는 경우
- 웹 전용 (모바일 앱 불필요)
- 세션 즉시 무효화가 중요한 경우

---

## 3. SUNNY ECOSYSTEM 맞춤 추천

### 3.1 현재 상황 분석

**서비스 구성**:
- 메인 페이지: `index.html` (SUNNY ECOSYSTEM 포털)
- HDH Fintech: `HDH_Fintech/index.html`
- ProActive Senior: `ProActive_Senior/index.html`
- HIPUS AI: 별도 서비스 (Coming Soon)
- Company Valuation: 별도 서비스 (Coming Soon)

**기술 스택**:
- 프론트엔드: Vanilla JavaScript, HTML, CSS
- 백엔드: 현재 없음 (정적 페이지)
- 배포: GitHub Pages 또는 정적 호스팅

**현재 문제점**:
1. 로그인 상태가 변수로만 관리 (영속성 없음)
2. 각 서비스 간 로그인 정보 공유 안 됨
3. 백엔드 없이 프론트엔드만 존재
4. 실제 사용자 데이터베이스 없음

### 3.2 단계별 구현 로드맵

#### Phase 1: 프로토타입 (1-2주) ⭐
**목표**: LocalStorage 기반 간단한 SSO 구현

**구현 내용**:
```javascript
// sso-core.js - 모든 페이지에서 공통으로 사용
const SSO = {
    // 로그인
    login(username, email, role = 'basic') {
        const userData = {
            username,
            email,
            role,
            loginTime: new Date().toISOString(),
            sessionId: this.generateSessionId()
        };
        localStorage.setItem('sunny_sso_session', JSON.stringify(userData));
        this.broadcastLoginEvent(userData);
    },

    // 로그아웃
    logout() {
        localStorage.removeItem('sunny_sso_session');
        this.broadcastLogoutEvent();
    },

    // 로그인 상태 확인
    isAuthenticated() {
        const session = localStorage.getItem('sunny_sso_session');
        if (!session) return false;

        const userData = JSON.parse(session);
        // 24시간 경과 확인
        const loginTime = new Date(userData.loginTime);
        const now = new Date();
        const hoursPassed = (now - loginTime) / (1000 * 60 * 60);

        if (hoursPassed > 24) {
            this.logout();
            return false;
        }

        return true;
    },

    // 사용자 정보 가져오기
    getUserData() {
        const session = localStorage.getItem('sunny_sso_session');
        return session ? JSON.parse(session) : null;
    },

    // 세션 ID 생성
    generateSessionId() {
        return 'session_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
    },

    // 다른 탭/창에 로그인 이벤트 전파
    broadcastLoginEvent(userData) {
        localStorage.setItem('sunny_sso_event', JSON.stringify({
            type: 'login',
            timestamp: Date.now(),
            data: userData
        }));
        localStorage.removeItem('sunny_sso_event'); // 이벤트 클리어
    },

    // 다른 탭/창에 로그아웃 이벤트 전파
    broadcastLogoutEvent() {
        localStorage.setItem('sunny_sso_event', JSON.stringify({
            type: 'logout',
            timestamp: Date.now()
        }));
        localStorage.removeItem('sunny_sso_event');
    },

    // 다른 탭/창의 로그인 상태 변경 감지
    onStorageChange(callback) {
        window.addEventListener('storage', (e) => {
            if (e.key === 'sunny_sso_event' && e.newValue) {
                const event = JSON.parse(e.newValue);
                callback(event);
            }
        });
    }
};

// 페이지 로드 시 로그인 상태 확인
document.addEventListener('DOMContentLoaded', () => {
    if (SSO.isAuthenticated()) {
        const user = SSO.getUserData();
        updateUIForLoggedInUser(user);
    } else {
        updateUIForLoggedOutUser();
    }

    // 다른 탭의 로그인 상태 변경 감지
    SSO.onStorageChange((event) => {
        if (event.type === 'login') {
            updateUIForLoggedInUser(event.data);
        } else if (event.type === 'logout') {
            updateUIForLoggedOutUser();
        }
    });
});
```

**장점**:
- 즉시 적용 가능
- 백엔드 불필요
- 구현 시간 최소화
- 프로토타입 검증에 적합

**적용 방법**:
1. `sso-core.js` 파일 생성
2. 모든 HTML 페이지에 `<script src="/sso-core.js"></script>` 추가
3. 기존 로그인/로그아웃 로직을 SSO API로 교체

---

#### Phase 2: MVP (1-2개월) ⭐⭐⭐
**목표**: JWT 기반 실제 인증 시스템 구축

**필요 인프라**:
1. Node.js 백엔드 서버
2. MongoDB 또는 PostgreSQL
3. 도메인 및 HTTPS

**구현 내용**:
- 사용자 회원가입/로그인 API
- JWT 발급 및 검증
- Refresh Token 관리
- 비밀번호 암호화 (bcrypt)
- 이메일 인증

**API 엔드포인트**:
```
POST   /api/auth/register      # 회원가입
POST   /api/auth/login         # 로그인
POST   /api/auth/logout        # 로그아웃
POST   /api/auth/refresh       # 토큰 갱신
GET    /api/auth/me            # 현재 사용자 정보
POST   /api/auth/verify-email  # 이메일 인증
POST   /api/auth/reset-password # 비밀번호 재설정
```

**프로젝트 구조**:
```
sunny-ecosystem-backend/
├── src/
│   ├── config/
│   │   └── database.js
│   ├── models/
│   │   └── User.js
│   ├── routes/
│   │   └── auth.js
│   ├── middleware/
│   │   └── authenticate.js
│   ├── utils/
│   │   ├── jwt.js
│   │   └── password.js
│   └── index.js
├── package.json
└── .env
```

---

#### Phase 3: 프로덕션 (3-6개월) ⭐⭐⭐⭐⭐
**목표**: 엔터프라이즈급 SSO 시스템

**구현 내용**:
- OAuth 2.0 완전 구현 또는 Keycloak 도입
- 소셜 로그인 (Google, Naver, Kakao)
- 2단계 인증 (2FA)
- 역할 기반 접근 제어 (RBAC)
- 감사 로그
- 세션 관리 대시보드
- 보안 강화 (Rate limiting, CAPTCHA 등)

---

## 4. 보안 고려사항

### 4.1 필수 보안 조치

#### 1. HTTPS 사용
```
❌ http://sunny-ecosystem.com
✅ https://sunny-ecosystem.com
```
모든 토큰 전송은 반드시 HTTPS를 통해야 합니다.

#### 2. XSS 방지
```javascript
// 나쁜 예
element.innerHTML = userInput;

// 좋은 예
element.textContent = userInput;
// 또는
const sanitized = DOMPurify.sanitize(userInput);
element.innerHTML = sanitized;
```

#### 3. CSRF 방지
```javascript
// CSRF 토큰 추가
<meta name="csrf-token" content="{{ csrf_token }}">

// API 요청 시 포함
fetch('/api/endpoint', {
    headers: {
        'X-CSRF-Token': document.querySelector('meta[name="csrf-token"]').content
    }
});
```

#### 4. 비밀번호 보안
```javascript
const bcrypt = require('bcrypt');
const saltRounds = 12;

// 해싱
const hashedPassword = await bcrypt.hash(plainPassword, saltRounds);

// 검증
const isValid = await bcrypt.compare(plainPassword, hashedPassword);
```

#### 5. JWT 보안
```javascript
// Secret Key는 환경변수로 관리
const SECRET_KEY = process.env.JWT_SECRET_KEY;

// 짧은 만료 시간
const accessToken = jwt.sign(payload, SECRET_KEY, { expiresIn: '15m' });

// Refresh Token은 더 긴 시간
const refreshToken = jwt.sign(payload, SECRET_KEY, { expiresIn: '7d' });
```

### 4.2 보안 체크리스트

- [ ] HTTPS 적용
- [ ] 비밀번호 해싱 (bcrypt, argon2)
- [ ] JWT Secret Key 환경변수 관리
- [ ] 토큰 만료 시간 설정 (Access: 15분, Refresh: 7일)
- [ ] XSS 방지 (입력 검증, sanitization)
- [ ] CSRF 방지 (토큰 사용)
- [ ] Rate Limiting (무차별 대입 공격 방지)
- [ ] SQL Injection 방지 (Prepared Statements)
- [ ] 민감 정보 로깅 금지
- [ ] CORS 적절히 설정
- [ ] 세션 타임아웃 설정
- [ ] 로그아웃 시 토큰 무효화
- [ ] 2FA 구현 (선택)
- [ ] 감사 로그 기록

---

## 5. 구현 우선순위 및 추천

### 5.1 즉시 적용 (1주일 내)
**방식**: LocalStorage 기반 SSO (Phase 1)

**이유**:
- 백엔드 없이 즉시 구현 가능
- 사용자 경험 즉시 개선
- 프로토타입 검증에 적합
- 다음 단계로 마이그레이션 용이

**작업 내용**:
1. `sso-core.js` 구현
2. 모든 페이지에 적용
3. 로그인 상태 UI 업데이트
4. 테스트 및 버그 수정

**예상 시간**: 3-5일

---

### 5.2 단기 목표 (1-2개월)
**방식**: JWT 기반 SSO (Phase 2)

**이유**:
- 실제 프로덕션에 사용 가능
- 보안성 확보
- 확장 가능한 아키텍처
- 업계 표준 방식

**작업 내용**:
1. Node.js 백엔드 구축
2. 데이터베이스 설계 및 구축
3. 인증 API 개발
4. 프론트엔드 통합
5. 테스트 및 배포

**예상 시간**: 4-8주

---

### 5.3 장기 목표 (3-6개월)
**방식**: OAuth 2.0 + 소셜 로그인 (Phase 3)

**이유**:
- 엔터프라이즈급 보안
- 다양한 외부 연동
- 세밀한 권한 관리
- 확장성 극대화

**작업 내용**:
1. Keycloak 또는 Auth0 도입 검토
2. 소셜 로그인 연동 (Google, Naver, Kakao)
3. RBAC 구현
4. 2FA 구현
5. 감사 로그 시스템
6. 관리자 대시보드

**예상 시간**: 12-24주

---

## 6. 비용 분석

### 6.1 LocalStorage 방식
- **개발 비용**: 무료 (내부 개발)
- **인프라 비용**: $0/월
- **유지보수**: 최소

### 6.2 JWT 방식
- **개발 비용**: 중간
- **서버 비용**: $10-50/월 (AWS EC2 t3.small, Heroku 등)
- **데이터베이스**: $15-30/월 (MongoDB Atlas, AWS RDS)
- **SSL 인증서**: $0 (Let's Encrypt)
- **합계**: **$25-80/월**

### 6.3 OAuth 2.0 (Keycloak 자체 호스팅)
- **개발 비용**: 높음
- **서버 비용**: $30-100/월 (더 높은 스펙 필요)
- **데이터베이스**: $30-50/월
- **합계**: **$60-150/월**

### 6.4 OAuth 2.0 (SaaS 사용)
- **Auth0**: $23/월 (최대 7,000명 사용자)
- **Okta**: $2/사용자/월
- **AWS Cognito**: $0.0055/활성 사용자/월

---

## 7. 마이그레이션 전략

### Phase 1 → Phase 2 마이그레이션

**1단계: 백엔드 구축**
- LocalStorage 방식과 병행
- 백엔드 API 완성 후 전환

**2단계: 점진적 전환**
```javascript
// 호환 레이어
const AuthService = {
    async login(username, password) {
        if (USE_BACKEND) {
            // JWT 방식
            const response = await fetch('/api/auth/login', {
                method: 'POST',
                body: JSON.stringify({ username, password })
            });
            const data = await response.json();
            localStorage.setItem('accessToken', data.accessToken);
        } else {
            // LocalStorage 방식 (기존)
            SSO.login(username, email, role);
        }
    }
};
```

**3단계: 완전 전환**
- LocalStorage 방식 제거
- JWT 방식으로 완전 전환

---

## 8. 테스트 계획

### 8.1 기능 테스트
- [ ] 로그인 성공
- [ ] 로그인 실패 (잘못된 비밀번호)
- [ ] 로그아웃
- [ ] 토큰 갱신
- [ ] 토큰 만료 처리
- [ ] 여러 탭에서 동시 로그인
- [ ] 한 탭에서 로그아웃 시 다른 탭도 로그아웃
- [ ] 페이지 새로고침 후 로그인 유지
- [ ] 서비스 간 로그인 상태 공유

### 8.2 보안 테스트
- [ ] XSS 공격 방어
- [ ] CSRF 공격 방어
- [ ] SQL Injection 방어
- [ ] 무차별 대입 공격 방어 (Rate limiting)
- [ ] 토큰 위조 감지
- [ ] 세션 하이재킹 방어

### 8.3 성능 테스트
- [ ] 동시 로그인 사용자 100명
- [ ] 동시 로그인 사용자 1,000명
- [ ] 토큰 검증 속도
- [ ] API 응답 시간

---

## 9. 모니터링 및 로깅

### 9.1 로깅 항목
```javascript
// 로그인 성공
logger.info('User logged in', {
    userId: user.id,
    username: user.username,
    ip: req.ip,
    userAgent: req.headers['user-agent'],
    timestamp: new Date()
});

// 로그인 실패
logger.warn('Login failed', {
    username: username,
    reason: 'Invalid password',
    ip: req.ip,
    timestamp: new Date()
});

// 토큰 갱신
logger.info('Token refreshed', {
    userId: user.id,
    timestamp: new Date()
});

// 로그아웃
logger.info('User logged out', {
    userId: user.id,
    timestamp: new Date()
});
```

### 9.2 모니터링 메트릭
- 로그인 성공/실패 비율
- 평균 세션 길이
- 동시 접속자 수
- 토큰 갱신 빈도
- API 응답 시간
- 에러 발생 빈도

### 9.3 알림 설정
- 로그인 실패 급증 (10분 내 100회 이상)
- API 응답 시간 초과 (>3초)
- 에러율 급증 (>5%)
- 서버 다운

---

## 10. 결론 및 권장사항

### 10.1 즉시 실행 (1주일)
✅ **LocalStorage 기반 SSO 구현 (Phase 1)**

**이유**:
- 빠른 프로토타입 검증
- 사용자 경험 즉시 개선
- 백엔드 구축 시간 확보
- 비용 0원

**다음 단계**:
- 사용자 피드백 수집
- 백엔드 개발 병행

---

### 10.2 단기 목표 (2개월)
✅ **JWT 기반 SSO 구현 (Phase 2)**

**이유**:
- 프로덕션 레벨 보안
- 실제 사용자 데이터 관리
- 확장 가능한 아키텍처
- 합리적인 비용 ($50/월 내외)

**준비사항**:
- Node.js 개발 리소스
- 데이터베이스 설계
- 서버 인프라
- 도메인 및 SSL

---

### 10.3 장기 비전 (6개월+)
✅ **OAuth 2.0 + 소셜 로그인 (Phase 3)**

**조건**:
- 사용자 1,000명 이상
- B2B 고객 확보
- 외부 서비스 연동 필요
- 예산 충분 ($150/월 이상)

---

## 11. 참고 자료

### 11.1 공식 문서
- [JWT.io](https://jwt.io/) - JWT 공식 사이트
- [OAuth 2.0](https://oauth.net/2/) - OAuth 공식 사이트
- [Keycloak Documentation](https://www.keycloak.org/documentation)
- [Auth0 Documentation](https://auth0.com/docs)

### 11.2 라이브러리
- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) - Node.js JWT
- [passport.js](http://www.passportjs.org/) - 인증 미들웨어
- [bcrypt](https://github.com/kelektiv/node.bcrypt.js) - 비밀번호 해싱
- [express-session](https://github.com/expressjs/session) - 세션 관리

### 11.3 보안 가이드
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
- [NIST Digital Identity Guidelines](https://pages.nist.gov/800-63-3/)

---

## 12. 다음 단계

### 즉시 수행할 작업:
1. ✅ 이 보고서 검토 및 승인
2. ⏭️ Phase 1 구현 시작 (LocalStorage SSO)
3. ⏭️ 백엔드 아키텍처 설계 (Phase 2 준비)
4. ⏭️ 개발 리소스 확보
5. ⏭️ 인프라 예산 책정

### 의사결정 필요 사항:
- [ ] Phase 1 구현 승인
- [ ] Phase 2 일정 및 예산 승인
- [ ] 백엔드 기술 스택 결정 (Node.js, Python, Java 등)
- [ ] 데이터베이스 선택 (MongoDB, PostgreSQL, MySQL)
- [ ] 호스팅 서비스 선택 (AWS, GCP, Heroku, Vercel)

---

**문서 끝**

작성자: Claude AI
버전: 1.0
최종 수정일: 2025-12-06
