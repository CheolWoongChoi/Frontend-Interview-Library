# 📆 210329 질문

## JavaScript
1. const와 var의 차이점은? (실행 컨텍스트 관점에서도 설명하기)
  - `var`은 ES6 이전부터 사용, `let`과 `const`는 ES6부터 등장
  - `var`은 함수 스코프, `let`과 `const`는 블록 스코프
  - `var`은 동일한 스코프 안에서도 재선언 가능
    - 코드의 가독성이 떨어질 수 있고, 에러 발생의 원인이 된다.
  - 반면, `let`과 `const`는 동일한 스코프에서 같은 키워드로 같은 변수를 재선언할 수 없다.
  - 실행 컨텍스트란, JS에서 코드가 어떻게 동작하는지 결정하는 환경을 의미한다.
    - 실행 컨텍스트라고도 하고, 어떤 곳에서는 환경 레코드라고 지칭한다.
    - 변수, 인자(arguments), this, 스코프 체인를 기억한다.
    - JS 스크립트가 실행될 때, 전역 컨텍스트가 생기고 함수가 생성될 때마다, 함수 컨텍스트가 생긴다.
  - 실행 컨텍스트가 생성되면, 내부의 변수, 함수 선언문이 위로 올라간다. (호이스팅)
  - `var`로 선언한 변수는 코드를 만나기 전에, 위에서 변수에 접근하면 undefined이 나온다.
  - `let`과 `const`도 호이스팅되지만, 코드를 만나기 전에 위에서 변수에 접근하면 error가 발생한다. (uninitialized 상태) 
  - `let`과 `const`가 선언된 코드를 JS에서 해석하면, undefined 값이 할당되고 해당 변수에 값이 할당되면, 해당 값이 들어간다.
  - `let`과 `const`의 경우, 호이스팅된 상태부터 코드를 만나기 전까지의 범위를 DZ(Dead Zone)이라고 한다. 또는 TDZ(Temporary Dead Zone), 일시적 사각 지대
  - 📌참고
  - [변수의 유효범위와 클로저, 모던 JavaScript 튜토리얼](https://ko.javascript.info/closure)
  - [실행 컨텍스트, ZeroCho 블로그](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)
  - [Execution Context, PoiemaWeb](https://poiemaweb.com/js-execution-context)

2. 동기 처리와 비동기 처리의 차이점을 설명해보세요.
  - 📌참고
  - [동기와 비동기방식의 차이점](https://blog.metafor.kr/164)
  - [이벤트 루프와 매크로,마이크로태스크](https://ko.javascript.info/event-loop#ref-1165)
3. High Order Function(고차 함수)란 무엇인가?
  - 📌참고
  - [자바스크립트 고차 함수(Higher-Order Function) 이해하기](https://velog.io/@jakeseo_me/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%9D%BC%EB%A9%B4-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A0-33%EA%B0%80%EC%A7%80-%EA%B0%9C%EB%85%90-22-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98Higher-Order-Function-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)

## Web
1. 웹 브라우저 url에 www.naver.com 를 입력했을 때, 화면이 나오기까지 일어나는 일을 설명해라.
  - 웹 브라우저가 url 해석
    - 프로토콜, 도메인, 포트를 해석
    - 올바른 url이면 요청 시작, 아닐 경우 웹 브라우저의 기본 검색엔진에 검색요청
  - HSTS(HTTP Strict Transport Security) 목록 확인
    - HSTS란 웹 사이트가 HTTPS로 통신해야 한다고 알리는 보안 기능
    - 해당 url이 목록에 존재하면(캐시되어 있는 경우) HTTPS로 통신
    - HTTP로 요청을 보냈더라도, HTTPS로 다시 요청을 보냄
  - 도메인 주소에 맞는 IP 주소를 찾는다
    - 도메인 주소는 사람에 익숙한 주소
    - 컴퓨터는 네트워크 통신을 할 때, IP 주소가 필요하다
    - 해당 도메인의 IP 주소가 브라우저 또는 Local DNS에 존재하면, 해당 IP 주소로 통신을 시작한다
      - 존재하지 않는 경우, DNS 서버에 IP 주소를 요청한다.
      - 먼저 root DNS 서버에 요청, 없다면 차상위 DNS 서버에 요청
      - www.naver.com의 경우, .com 도메인을 관리하는 DNS 서버에 먼저 요청, 못 찾으면 naver.com 도메인을 관리하는 DNS 서버에 요청
      - IP 주소를 찾으면 Local DNS는 해당 IP 주소를 캐싱하고 응답
  - IP 주소를 이용해서, 라우터를 통해 www.naver.com 서버까지의 경로를 파악
  - 네트워크 통신을 하기 위해서 IP 주소와 MAC 주소가 필요
    - IP 주소는 논리 주소, MAC 주소는 물리 주소
    - MAC 주소는 각 노드(컴퓨터)의 네트워크 인터페이스를 지칭한다. NIC(Network Interface Card)에 할당된 고유 식별 주소 또는 고유 식별자
    - ARP(Address Resolution Protocol)을 통해 서버의 MAC 주소를 알아낸다.
    - 내 컴퓨터에서 naver 서버까지 네트워크 통신은 여러 노드들을 거치게 될 것이다.
    - ARP를 통해 각 노드들과 네트워크 통신하면서 naver 서버로 패킷을 전달하는 것이다.
  - HTTP 통신을 하기 위해서는 TCP 커넥션이 되어야 한다.
    - TCP 통신을 하기 위해서는 Socket 통신이 필요하며 클라이언트 IP와 포트번호, 서버의 IP와 포트번호 이 4가지 정보를 통해 1:1 매칭이 된다.
    - TCP는 3 handshaking을 통해 연결이 결정된다.
      - 클라이언트에서 Syn 패킷
      - 서버에서 Syn + Ack 패킷
      - 클라이언트가 다시 Ack 패킷
      - TCP 연결 완료
    - HTTPS 통신이라면, TCP 커넥션 후에 TLS(SSL) handshaking이 일어난다.   
  - TCP 커넥션이 성공하면, 그 이후로 HTTP 트랜잭션(요청과 응답)이 발생한다.
  - HTTP 요청/응답 
    - HTTP 요청 메시지는 첫째줄에 HTTP 메소드 / URL / HTTP 버전, 둘째줄에 HTTP 헤더, 셋째줄에 엔티티(데이터)로 구성 
    - HTTP 응답 메시지는 첫째줄에 상태코드 / 상태 메시지 / HTTP 버전, 둘째줄에 HTTP 헤더, 셋째줄에 엔티티(데이터)로 구성
    - OSI 계층
      - 상위 계층에서 하위 계층으로 데이터가 계층을 지날 때마다 캡슐화되고, 네트워크를 통해 전달될 노드로 이동
      - 해당 데이터를 받은 노드는 하위 계층에서 상위 계층으로 데이터를 디캡슐화하면서 전달
      - HTTP 메시지는 애플리케이션 계층(7계층)에서 생성
      - TCP 세그먼트는 전송 계층 (4계층)에서 만들어지며, 클라이언트 포트와 서버 포트를 헤더에 포함시키고, HTTP 메시지를 가지고 있다.
      - IP 데이터그램(패킷)은 네트워크 계층 (3계층)에서 만들어지고, 클라이언트 IP주소와 서버 IP주소를 헤더에 포함시키고, TCP 세그먼트를 포함
      - 링크 계층(2계층)에서는 MAC 주소를 헤더에 포함시키고, 패킷을 가지고 있다.
      - 물리적 계층을 통해 네트워크에 접속해서 패킷을 전달
  - 📌참고
    - [브라우저에 URL을 입력했을 때 발생하는 일들](https://deveric.tistory.com/97)
    - [웹 브라우저에 URL을 입력하면 어떤 일이 일어날까?](https://owlgwang.tistory.com/1)
    - 그림으로 배우는 Http & Network Basic
    
2. 프레임워크와 라이브러리의 차이점
  - 📌참고
  - 여러 포스팅을 확인했지만, 아래 포스팅이 원래 작성한 글인 듯하다.
  - [프레임워크와 라이브러리의 차이점](https://webclub.tistory.com/458)
3. 크로스 브라우징 이슈에 대응하는 방법을 설명해주세요.
  - 📌참고
  - [크로스 브라우징](https://velog.io/@seochanh/00003)

## React
1. useCallback은 언제 사용하는가?
2. 클래스형 컴포넌트와 함수형 컴포넌트의 차이는 무엇인가?
3. JSX란?
