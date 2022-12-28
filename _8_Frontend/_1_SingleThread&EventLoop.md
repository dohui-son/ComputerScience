## Javascript는 어떤 언어인가요?

- 싱글 스레드 언어입니다. (동기적, synchronous)
- Javascript 엔진은 하나의 메모리힙과 단일 콜스택Call Stack(호출 스택)을 가지고 있습니다. 따라서 구조상 한번에 하나의 태스크(함수)만 동기적으로 실행 가능합니다.

- 즉, 하나의 메인스레드에서 호출되는 함수들이 콜스택에 쌓일것이고, 이 함수들은 LIFO방식으로 실행됩니다. Javascript가 싱글스레드 기반 언어라는 것은 Javascript가 단일 메인스레드, 단일 콜스택을 갖고 있기 때문입니다.
- 논블로킹, 이벤트드리븐

## 하지만 실제 사용시에는 멀티 스레드 처럼 사용하는데 어떻게 사용하나요? (어떻게 비동기적으로 작동하는 것인가요?)

- Javascript는 싱글스레드 언어이지만, 런타임은 멀티스레드입니다.
- Javascript 엔진만 독립적으로 실행되지않고, 웹브라우저나 Node JS와 같은 멀티스레드 환경에서 실행되게 됩니다. (환경에 임베디드되어 실행)
- 특히 런타임 영역(브라우저, node JS)의 Web API, callback queue, event loop를 통해 비동기 방식으로 동시성을 지원합니다.
- setTimeout이나 ajax같은 비동기 함수가 호출되면, 해당 태스크는 브라우저의 Web API에게 넘겨집니다. Web API에서 코드가 실행될 준비가 되면 callback queue에 해당 작업을 넣어줍니다. 그래서 사실상 비동기 함수가 동기적인 함수들과 '동시'에 동작하는 것처럼 보이지만, 그 비동기 함수들이 재빠르게 콜 스택에 추가되어 실행되었기 때문에 동시에 실행된다고 착각하는 것입니다.

## 비동기적으로 실행이 되는 것을 동기적으로 코딩하는 방법이 있나요?

- callback, promise, async/await를 통해 비동기적인 함수를 동기적으로 활용할 수 있습니다.
- [ callback ] 먼저 callback을 설명드리자면, 콜백함수는 특정 함수에 인자로 전달된 함수를 의미합니다. 자바스크립트의 함수는 일급객체이기에 매개변수로 함수를 사용할 수 있습니다.
- 콜백함수는 함수를 등록하기만 하고 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 콜백함수를 호출하게 됩니다.
- 이렇게, 다른 함수가 실행을 끝낸뒤 콜백함수가 실행되게 할 수 있기에 비동기적 함수를 동기적으로 처리할 때도 사용될 수 있습니다.
- 콜백의 단점으로 callback hell을 꼽을 수 있습니다.
- [ promise ] 프로미스는 자바스크립트 ajax나 setTimeout과 같은 비동기 처리에 사용되는 객체입니다.
- promise는 callback hell을 promise로 해결 할 수 있습니다. 또한 promise chaining으로 여러 개의 프로미스를 연결하여 사용할 수도 있습니다. promise 코드가 콜백에 비해 패턴이 정형식화 되어있어서 callback보다 상대적으로 가독성이 뛰어납니다.
- 프로미스는 3가지 상태를 갖습니다. 이 상태란 프로미스 처리 과정을 의미하는테, 프로미스는 생성하고 종료될 때까지 3가지 pending(대기) / fulfilled(이행) / rejected(실패) 상태를 갖습니다.

- new Promise() 메서드를 호출하면 pending(대기) 상태가 됩니다.
- new Promise(function(resolve,reject){}) 메서드를 호출할 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자로 resolve, reject를 사용할 수 있습니다.
- 이 resolve를 실행하면, fulfilled(이행, 완료) 상태가 되기에 then()을 이용하여 처리 결과값을 받을 수 있습니다. reject를 호출하면 reject(실패)상태가 됩니다. reject 상태가 되면 catch로 실패 처리 결과 값(err)을 받을 수 있습니다.

```Javascript
function getData(callback) {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      resolve(response); // 데이터를 받으면 resolve() 호출
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function(tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});

```

```Javascript
function getData() {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData().then(function(data) {
  console.log(data); // response 값 출력
}).catch(function(err) {
  console.error(err); // Error 출력
});

```

- [ async / await ] aysnc와 await은 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법입니다.
- 콜백 함수와 프로미스의 단점을 보완하고

## Event Loop 에 대해서 알고 있으신가요?

## 마이크로태스크 큐와 태스크 큐에 대해서 말씀해주세요.

## ETC

### 논블로킹, 이벤트 드리븐?

### 일급객체

### callback, promise, async/await 차이점

**REFERENCE**

- https://velog.io/@eamon3481/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%B1%EA%B8%80%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%B8%EB%8D%B0-%EC%99%9C-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%A0%81-%EC%9D%BC%EA%B9%8C
- https://hongchangsub.com/javascript-asyncandsync/
- https://velog.io/@ko1586/Callback%ED%95%A8%EC%88%98%EB%9E%80-%EB%AD%94%EB%8D%B0
- https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
- https://springfall.cc/post/7
