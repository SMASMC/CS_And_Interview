## HTTP status code

> 클라우드 환경에서 HTTP API를 통해 통신하는 것이 대부분
> 
> 
> 이때, 응답 상태 코드를 통해 성공/실패 여부를 확인할 수 있으므로 API 문서를 작성할 때 꼭 알아야 할 것이 HTTP status code다
> 
- 10x : 정보 확인
- 20x : 통신 성공
- 30x : 리다이렉트
- 40x : 클라이언트 오류
- 50x : 서버 오류

**200번대 : 통신 성공**

| 상태코드 | 이름 | 의미 |
| --- | --- | --- |
| 200 | OK | 요청 성공(GET) |
| 201 | Create | 생성 성공(POST) |
| 202 | Accepted | 요청 접수O, 리소스 처리X |
| 204 | No Contents | 요청 성공O, 내용 없음 |

**300번대 : 리다이렉트**

| 상태코드 | 이름 | 의미 |
| --- | --- | --- |
| 300 | Multiple Choice | 요청 URI에 여러 리소스가 존재 |
| 301 | Move Permanently | 요청 URI가 새 위치로 옮겨감 |
| 304 | Not Modified | 요청 URI의 내용이 변경X |

**400번대 : 클라이언트 오류**

| 상태코드 | 이름 | 의미 |
| --- | --- | --- |
| 400 | Bad Request | API에서 정의되지 않은 요청 들어옴 |
| 401 | Unauthorized | 인증 오류 |
| 403 | Forbidden | 권한 밖의 접근 시도 |
| 404 | Not Found | 요청 URI에 대한 리소스 존재X |
| 405 | Method Not Allowed | API에서 정의되지 않은 메소드 호출 |
| 406 | Not Acceptable | 처리 불가 |
| 408 | Request Timeout | 요청 대기 시간 초과 |
| 409 | Conflict | 모순 |
| 429 | Too Many Request | 요청 횟수 상한 초과 |

**500번대 : 서버 오류**

| 상태코드 | 이름 | 의미 |
| --- | --- | --- |
| 500 | Internal Server Error | 서버 내부 오류 |
| 502 | Bad Gateway | 게이트웨이 오류 |
| 503 | Service Unavailable | 서비스 이용 불가 |
| 504 | Gateway Timeout | 게이트웨이 시간 초과 |