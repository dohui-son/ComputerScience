# 1\. HTML, CSS, Javascript에 대해서 설명하세요.

```
HTML은 웹페이지를 제목, 이미지, 표 등으로 정의하고 '구조와 의미를 부여'하는 '정적 언어'입니다.
웹의 '전체적인 구조'를 담당하고 있습니다.
CSS는 HTML이 실제 표시되는 스타일인 색상, 레이아웃, 크기, 폰트 등을 지정하여 '콘텐츠를 꾸미는 정적 언어'입니다.
웹의 시각적인 표현을 담당합니다.
Javascript는 HTML의 정적이고 단조로운 한계를 극복하기 위해 만들어진 언어입니다.
'웹문서를 동적으로 처리'할 수 있도록 도와줍니다.
```

# 2\. 쿠키에 대해 설명해주세요.

```
쿠키란 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일입니다.
사용자 인증이 유효한 시간을 명시할 수 있고, 유효 시간이 정해지면 브라우저가 종료되어도 인증이 유지되는 특징이 있습니다.
쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조합니다.
Response Header에 Set-Cookie 속성을 사용하면 클라이언트에 쿠키를 만들 수 있고 
자동으로 Request시에 RequestHeader에 넣어 서버에 전송합니다.
방문한 사이트에 로그인 했을 때, "아이디와 비밀번호를 저장하시겠습니까?" 혹은 쇼핑몰의 장바구니에 해당됨. 
```

# 3\. 세션의 동작 방식을 설명해주세요.

```
1. 클라이언트가 서버에 접속시 세션 ID를 발급 받습니다.
2. 클라이언트는 세션 ID에 대해 쿠키를 사용해서 저장하고 가지고 있습니다.
3. 클라이언트는 서버에 요청할 때, 이 쿠키의 세션 ID를 같이 서버에 전달해서 요청합니다.
4. 서버는 세션 ID를 전달 받아서 별 다른 작업 없이 세션 ID로 세션에 있는 클라이언트 정보를 가져와서 사용합니다.
5. 클라이언트 정보를 가지고 서버요청을 처리하여 클라이언트에게 응답합니다.
```

------------------------------------------------------------

# 4\. 세션과 쿠키를 비교해주세요.

```
기본적으로 HTTP 프로토콜 환경은 connectionless, stateless한 특성을 가지기에 
서버는 클라이언트가 누구인지 매번 확인해야합니다.
세션은 쿠키를 기반으로 동작하지만 쿠키는 서버 자원을 사용하지 않고 세션은 서버 자원을 사용합니다.
보안적으로 쿠키보다 세션이 상대적으로 조금 더 낫다고 말할 수 있습니다.
쿠키는 클라이언트 로컬에 저장되기에 변질되거나 request에서 스니핑 당할 우려가 있습니다. 
하지만 세션은 쿠키를 이용해서 session id 만 저장하고 이를 서버에서 처리하기에 상대적으로 보안성이 좋다고 할 수 있습니다.
쿠키는 만료시간이 있지만 파일로 저장되기에 브라우저를 종료해도 계속 정보가 남아있을 수 있습니다.
반면 세션도 만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간과 상관없이 삭제됩니다.
예를 들어 크롬에서 다른 탭을 사용해도 세션을 공유할 수 있습니다. 
다른 브라우저를 사용하게 되면 다른 세션을 사용할 수 있습니다.
세션은 서버의 자원을 사용하기에 무분별하게 만들면 서버의 메모리를 감당 할 수 없게 되고 속도가 느려질 수 있습니다.

*connectionsless : 클라이언트가 요청을 한 후 응답을 받으면 연결을 끊어버리는 특징. 
HTTP는 먼저 클라이언트가 request를 서버에 보내면, 서버는 클라이언트에게 요청에 맞는 response 를 보내고 접속을 끊음.
*stateless :  통신이 끝나면 상태를 유지하지 않는 특징. 
연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보는 유지하지 않는 특성이 있음.
*스니핑 : 네트워크 상에서 자신이 아닌 타인의 패킷 교환을 엿듣는 것.
```

# 5\. 왜 프로젝트에 리액트 라이브러리를 사용하셨나요?

```
먼저, 리액트는 캡슐화된 컴포넌트 기반으로 화면을 구성하기에 
기능에 따른 컴포넌트 관리, 컴포넌트 재사용 등이 용이 했습니다.
처음부터 요구명세서가 갖춰지지 않은 상태에서 
프로젝트를 진행할 때는 페이지의 세부 기획 사항이 자주 수정되었습니다.
이러한 프로젝트 진행 방식에서는 
역할 및 기능별로 나뉘어져 있는 컴포넌트로 개발을 진행하는 것이 매우 유리했습니다.

또한 리액트의 Virtual DOM으로 인한 빠른 리랜더링 때문에 리액트로 개발을 진행했습니다.
리액트는 가상 DOM을 이용하여 실제 DOM 조작 횟수를 줄여 성능을 빠르게 개선했습니다.
따라서 사용성을 높이기 위해 프론트엔드 라이브러리로 리액트를 채택했습니다.

(+ 추가 답변 : 단방향 데이터 바인딩. 
데이터가 변경되면 리액트는 가상 DOM을 변경합니다. 
그리고 이전의 가상 DOM과 비교하여 변경된 부분을 체크하고 변경된 부분만
실제 DOM에 적용합니다. 
이렇게 가상 DOM을 이용해 실제 DOM 조작 횟수를 줄여 성능을 빠르게 개선합니다. 
이러한 동작 방식으로 인해 애플리케이션의 규모가 클수록, 
데이터 변경이 많을 수록 더 뛰어난 성능을 발휘합니다. )
```