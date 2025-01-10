## OAuth1.0과 OAuth2.0

**OAuth 1.0(Open Authorization)**

- **OAuth**는 애플리케이션이 사용자 정보를 **사용자 비밀번호를 요구하지 않고** 제3의 서비스(예: Google, Facebook)로부터 안전하게 접근할 수 있도록 인증을 제공하는 **권한 부여 프레임워크이다.**
- 주로 **로그인**이나 **API 접근**에 사용된다

**OAuth 2.0**

- OAuth의 개선된 버전으로, 보안과 사용 편의성을 강화한 프레임워크
- 클라이언트 애플리케이션, 서버 간의 통신을 분리하고 **다양한 인증 흐름**을 제공

**OAuth 1.0의 흐름**

1. **Request Token 요청:** 클라이언트가 Consumer Key와 Secret으로 Request Token을 요청하고, 서버가 Request Token과 Secret을 반환.
2. **사용자 권한 승인:**
    
    사용자가 인증 서버에 로그인하여 Request Token을 승인하고, 서버가 Verifier(검증 코드)를 클라이언트에 전달.
    
3. **Access Token 요청:**
    
    클라이언트가 Request Token과 Verifier를 사용해 Access Token을 요청하고, 서버가 Access Token과 Secret을 반환.
    
4. **자원 접근:**
    
    클라이언트가 Access Token을 사용해 자원 서버(API)에서 사용자 데이터를 요청하고, 서버가 데이터를 반환.
    

**OAuth 2.0의 주요 흐름 (Authorization Code Flow)**

1. **사용자 로그인 요청:**
    
    사용자가 클라이언트 앱에서 인증 요청.
    
2. **클라이언트 → 인증 서버:**
    
    클라이언트가 인증 서버에 권한 요청, 사용자가 권한 승인.
    
3. **Authorization Code 반환:**
    
    인증 서버가 클라이언트에 Authorization Code를 전달.
    
4. **클라이언트 → 인증 서버 (토큰 요청):**
    
    클라이언트가 Authorization Code를 사용해 Access Token을 요청.
    
5. **Access Token 발급:**
    
    인증 서버가 클라이언트에 Access Token을 반환.
    
6. **클라이언트 → 자원 서버:**
    
    클라이언트가 Access Token으로 자원 서버에 데이터 요청.
    
7. **자원 반환:**
    
    자원 서버가 클라이언트에 사용자 데이터를 반환.
    

**OAuth 1.0과 OAuth 2.0의 주요 차이**

| **항목** | **OAuth 1.0** | **OAuth 2.0** |
| --- | --- | --- |
| **보안 방식** | 요청마다 암호화된 **서명(Signature)** 필요 | HTTPS로 보안을 유지하며 **Access Token**만 사용 |
| **흐름의 복잡성** | Request Token, Access Token, Secret 키 등 단계가 많음 | Authorization Code, Access Token만 사용해 더 간단함 |
| **통신 프로토콜** | HMAC-SHA1, RSA-SHA1 등으로 요청 서명 | HTTPS를 통한 통신 |
| **토큰 유형** | Request Token, Access Token, Secret 등 다양한 토큰 사용 | Access Token, Refresh Token |
| 인증 흐름 | 고정된 흐름 | 다양한 인증 흐름 지원 |
| **유연성** | 단일 흐름만 지원 | 다양한 인증 흐름 제공 (Authorization Code, Implicit 등) |
| **사용성** | 구현이 복잡하고 사용자 경험이 부족 | 간단하고 모바일/웹 환경에 적합 |