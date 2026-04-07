# HTTP 관련

## HTTP, HTTPS 차이

HTTP는 평문 데이터를 전송해 도청과 위변조에 취약하다. 포트 80을 사용한다.

HTTPS는 HTTP에 TLS를 적용한것으로 포트 443을 쓴다.

**TLS가 보장하는 세가지**
1. 암호화 : 제 3자가 내용을 못본다.
2. 인증 : 인증서를 통해 서버 신원을 확인한다.
3. 무결성 : 전송 중 데이터 변조를 감지한다.

**TLS 핸트셰이크 흐름**
1.	ClientHello로 지원 가능한 TLS 버전과 암호화 방식을 보낸다.
2.	ServerHello와 Certificate로 서버가 방식 선택과 인증서를 전달한다.
3.	클라이언트가 인증서를 검증한다.
4.	키 교환으로 세션 키를 안전하게 합의한다.
5.	이후 세션 키로 대칭키 암호화 통신을 한다.

## HTTP/1.1, HTTP/2, HTTP/3

**HTTP/1.1**

- 요청을 순서대로 처리
- Keepalive로 TCP 연결 재사용 가능
- 브라우저당 동시 연결 수 제한으로 우회

**HTTP/2**

- 하나의 TCP 연결에서 여러 요청 동시 처리
- 헤더 압축으로 오버헤드 감소
- 클라이언트 요청 전에 리소스를 미리 전송
- 하지만 TCP 레벨의 HOL Blocking은 여전히 존재

**HTTP/3**

- UDP 기반의 QUIC 프로토콜 사용
- TCP 자체를 버려 TCP HOL Blocking을 근본적으로 해결
- 연결 수립이 빠름
- 패킷 손실 시 해당 스트림만 영향 받음

> HOL Blocking : 먼저 와야할 데이터가 늦어지거나 손실되면, 뒤에 온 데이터도 바로 처리하지 못하고 함께 기다리는 형상

## GET, POST 차이

**GET**

- 리소스를 조회할 떄 사용
- 데이터가 URL 쿼리스트링에 포함 -> 브라우저 히스토리, 서버 로그에 노출
- 멱등성O (같은 요청을 보내도 서버 최종상태가 같음), 안정성O (서버의 상태를 변경하지 않음)

**POST**

- 리소스를 조회할 때 사용
- 데이터가 HTTP Body에 담김 -> URL 미노출
- 멱등성X
- 캐싱 안됨

## HTTP 상태 코드

1xx (정보): 요청 처리 중 (거의 안 씀)

2xx (성공):
- 200 OK: 성공
- 201 Created: 리소스 생성 성공 (POST 응답)
- 204 No Content: 성공했지만 응답 바디 없음 (DELETE, PUT 응답)

3xx (리다이렉션):
- 301 Moved Permanently: 영구 이동 (검색엔진이 URL 교체)
- 302 Found: 임시 이동
- 304 Not Modified: 캐시 유효, 바디 없이 캐시 사용

4xx (클라이언트 오류):
- 400 Bad Request: 잘못된 요청 형식
- 401 Unauthorized: 인증 안 됨 (로그인 필요)
- 403 Forbidden: 인증은 됐지만 권한 없음
- 404 Not Found: 리소스 없음
- 409 Conflict: 상태 충돌 (중복 가입 등)
- 422 Unprocessable Entity: 유효성 검사 실패
- 429 Too Many Requests: 요청 횟수 초과 (Rate Limit)

5xx (서버 오류):
- 500 Internal Server Error: 서버 내부 오류
- 502 Bad Gateway: 프록시/게이트웨이 오류
- 503 Service Unavailable: 서버 과부하 또는 점검 중