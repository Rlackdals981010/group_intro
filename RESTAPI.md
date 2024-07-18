본 프로젝트의 기능
1. 각자 정보가 담긴 조원을 생성한다.
2. 저장된 조원을 조회한다.
3. 조원의 정보를 수정한다.
4. 조원을 삭제한다.

위 기능을 REST API로 제작하기 위해선 REST의 구성 3가지를 만족하도록 분석해야한다.

대표적으로 1의 경우를 `자원 : 조원` ,`행위(메서드) : 생성)`,`메시지 : 각자 정보가 담긴 `로 분석이 가능하다.
이 요청은 client가 server에 요청을 하는것이기 때문에 HTTP 요청 메시지를 통해서 서버에 리소스를 생성하게 된다.

HTTP 메시지는 다음과 같은 구조를 지닌다
> 1. start - line 
> 2. HTTP 헤더
> 3. CRLF
> 4. message-body (요청의 경우 생략 가능)

#### 1. start-line
>http 메서드 /요청메시지 HTTP 버전

start-line은 http 메시지의 최상단에 위치하며 위에 적힌 구성으로 작성된다. 그렇다면 본 프로젝트의 기능 1의 start-line은 다음과 같이 작성할 수 있다.
`POST /members/ HTTP/1.1`

#### 2. HTTP 헤더
`field-name: field-value`
HTTP 헤더는 start-line 다음줄에 위치하며 위에 적힌 구성으로 작성된다.

본 프로젝트는 아직 배포하지 않았기때문에 다음과 같이 작성할 수 있다.
`Host: localhost`

또한 데이터가 JSON 형식이기 때문에 요청 본문이 JSON형식임을 알려야한다.
`Content-Type: application/json`

#### 3. CRLF
단순한 개행문자다. 공백으로 생각하면 된다.

#### 4. message-body
 실제 전송할 데이터가 들어간다. 본 프로젝트의 기능 1의 경우 다음과 같이 작성할 수 있다.
 

```
{
    "members": {
        "name": "김창민",
        "blog": "https://velog.io/@rlackdals_98/posts",
        "MBTI" : "INFJ",
        "TMI" : "안녕하세요"
    }
}
```
위와 같은 형태는 JSON 형태로 작성된 데이터이다.


### 결과

```
POST /members/ HTTP/1.1
Host: localhost
Content-Type: application/json

{
    "members": {
        "name": "김창민",
        "blog": "https://velog.io/@rlackdals_98/posts",
        "MBTI": "INFJ",
        "TMI": "안녕하세요"
    }
}
```
 
 이런 형태로 구현을 진행하면 된다.