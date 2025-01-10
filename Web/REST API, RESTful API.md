## REST API, RESTful API

**REST (Representational State Transfer)**

- REST는 HTTP 프로토콜을 기반으로 자원을 관리하고 통신하기 위한 아키텍처 스타일이다
- 자원을 URI로 표현
ex)https://example.com/users/123
- HTTP 메서드 사용
GET, POST, PUT, DELETE

**RESTful API**

- REST의 원칙을 준수하여 설계된 API를 RESTful API라고 한다.
(REST원칙을 따라는 API이다.)

**REST API와 RESTful API의 차이점**

| **항목** | **REST API** | **RESTful API** |
| --- | --- | --- |
| **개념** | REST 아키텍처 스타일을 따르는 API | REST 원칙을 더욱 철저히 준수한 REST API |
| **REST 원칙 준수 여부** | REST 원칙을 완전히 지키지 않을 수도 있음 | REST 원칙을 최대한 준수하려는 API |
| **사용 예시** | 단순히 HTTP 요청/응답 형태만 따른 API | HTTP 메서드, URI 설계, 상태 관리 등을 잘 준수한 API |

**REST 특징 주요 3가지**

- **Statelessness (무상태성):** 상태 정보 저장 안 함 → 독립적 요청.
- **Resource-Oriented (자원 중심 설계):** URI로 자원 식별 → HTTP 메서드로 조작.
- **Uniform Interface (일관된 인터페이스):** 표준화된 형식 → 모든 플랫폼에서 사용 가능.