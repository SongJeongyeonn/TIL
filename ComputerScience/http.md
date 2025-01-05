# HTTP: 하이퍼텍스트 전용 프로토콜

## 특징
### 클라이언트-서버 구조 (Request-Response 구조)
- 클라이언트가 요청(HTTP 메시지)을 서버로 보내면, 서버는 결과를 만들어 클라이언트에 응답
  
### 무상태 프로토콜 (Stateless)
- 서버가 클라이언트의 상태를 보존하지 않음
  - **장점**: 서버 확장성이 높음 (스케일 아웃 가능)
  - **단점**: 클라이언트가 추가 데이터를 전송해야 하므로 데이터 사용량 증가.

### 비연결성 (Connectionless)
- 응답이 초 단위 이하로 빠르며, 서버 자원을 효율적으로 사용

---

## HTTP 메시지 구조
1. **시작 라인 (Start-Line)**
   - 요청 메시지: `method SP request-target SP HTTP-version CRLF`
   - 응답 메시지: `HTTP-version SP status-code SP reason-phrase CRLF`

2. **헤더 (Header)**
   - 모든 부가정보를 담고 있음
     - 형식: `field-name: OWS field-value OWS`

3. **공백 줄 (Empty Line)**
   - 헤더와 바디를 구분

4. **메시지 바디 (Message Body)**
   - HTML, JSON, 영상 등 전송할 데이터가 포함됨

---

## HTTP 메서드
### 주요 메서드
1. **GET**: 리소스 조회
   - 요청 데이터는 주로 쿼리 파라미터로 전달
   - 메시지 바디를 사용하지 않는 것을 권장
   ```http
   GET /search?q=hello&hl=ko HTTP/1.1
   Host: www.google.com
2. **POST**: 요청 데이터 처리 및 등록
- 메시지 바디를 통해 데이터 전달
- 용도
    1. 새 리소스 생성
    2. 요청 데이터 처리
    3. 다른 메서드로 처리하기 애매할 때
    ```http
    POST /members HTTP/1.1
    Content-Type: application/json
    {
        "username": "hello",
        "age": 20
    }
    ```
3. **PUT**: 리소스 대체
- 리소스가 있으면 대체, 없으면 새로 생성
  ```http
  PUT /members/100 HTTP/1.1
  Content-Type: application/json
  {
    "username": "hello",
    "age": 20
  }
  ```
4. **PATCH**: 리소스 부분 변경
   ```http
   PATCH /members/100 HTTP/1.1
   Content-Type: application/json
   {
    "age": 50 
   }
   ```
5. **DELETE**: 리소스 삭제
   ```http
   DELETE /members/100 HTTP/1.1
   Host: localhost:8080
   ```

#### 기타 메서드
- **HEAD**: GET과 동일하나 메시지 바디 제외
- **OPTIONS**: 리소스의 통신 가능 옵션 설명
- **CONNECT**: 터널 설정
- **TRACE**: 메시지 루프백 테스트

### HTTP 메서드 속성
1. **안전 (Safe)**: 호출해도 리소스 변경 없음

- 예: GET

2. **멱등 (Idempotent)**: 여러 번 호출해도 결과 동일

- 예: GET, PUT, DELETE

3. **캐시 가능 (Cacheable)**: 응답 결과를 캐시 가능

- 예: GET, HEAD, 일부 POST, PATCH

### 데이터 전송 방식
1. **쿼리 파라미터**
- 주로 GET 메서드 사용
- 검색, 필터링, 정렬 등에 활용

2. **메시지 바디**
- POST, PUT, PATCH 메서드 사용
- 회원가입, 주문 등 데이터 등록/변경에 사용