# 📆 210426 질문

## JavaScript
### ES6 이후에 나온 문법 중, 유용한 문법은 무엇이 있는가?
  - Optional Chaining (ES11)
    - `?.` 연산자를 의미한다.
    - 아래와 같은 에러를 방지할 수 있다.
      ```javascript
      person.def.asd;
      // 에러
      VM370:1 Uncaught TypeError: Cannot read property 'asd' of undefined at <anonymous>:1:12
      ```
    - 참조한 property가 nullish(`null` 또는 `undefined`)라면 에러 대신 undefined를 리턴한다.
    - 참조한 property가 존재하면, 해당 값을 리턴한다.
    - 기존에 `삼항 연산자` 또는 `&&` 연산자로 에러를 방지할 수 있었다. 하지만 코드가 중복되거나 길어지는 단점이 존재했다. 이를 `?.`연산자를 이용해 해결할 수 있다. 
      ```javascript
        const person = {
          name: 'CCW',
          job: {
            title: 'Frontend Engineer',
            manager: {
              name: 'Fortuna'
            }
          }
        };

        // 문제의 코드
        const m1 = person.job && person.job.manager && person.job.manager.name;
        const m2 = person.job 
                    ? person.job.manager
                      ? person.job.manager.name
                      : undefined
                    : undefined

        // Optional Chaining
        const m3 = person?.job?.manager?.name;
      ```
  - Nullish Coalescing Operator (ES11)
    - Null 병합 연산자로 번역됨. 영어는 잘 이해가 안가는 말인듯.  
    - 왼쪽 피연산자가 `null` 또는 `undefined`일 때, 오른쪽 피연산자를 반환한다. 그렇지 않으면, 왼쪽 피연산자를 반환한다.
    - `||` 연산자와는 달리 `null`과 `undefined`말고 다른 `falsy`값은 반환된다. (`''` 또는 `0`)
    - 그런데, 만약 `falsy`값을 사용하도록 고려했다면 (`||`의 경우 오른쪽 피연산자를 반환하도록 했다면) `Null 병합 연산자`를 사용해선 안된다.  
      ```javascript
        const name1 = null ?? 'default string';
        console.log(name1); // 'default string';

        const name2 = '' ?? 'default string';
        console.log(name2); // ''

        // React jsx에서
        const imgUrl = '' ?? 'imgUrl2';
        <img src={imgUrl} ... /> // 이미지를 불러올 수 없어서 에러가 발생한다.
      ```

  
### 자바스크립트 콜백함수에 대해서 설명해보세요.

## 자율 카테고리
### atomic 디자인 패턴에 대해서 서로 알아보고 이야기해보기
  - UI를 단위를 잘게 쪼갠 패턴, 일종의 컴포넌트 단위의 패턴이라고 볼 수 있음
  - 화학에서 용어를 가져와서 원자(Atoms), 분자(Molecules), 유기체(Organisms), 템플릿(Templates), 페이지(Pages) 단위(폴더)로 나눔
  - 개발뿐만 아니라 기획/디자인과 함께 적용해야 하는 패턴 또는 방법론
  - 러닝 커브가 높은 편이다.

  - 장점은 시스템을 잘 구축해놓으면, 테스팅, 디버깅, 유지보수가 편할 것이다.
  - `분자`는 `원자`를 2~3개 가져다 쓰는 것이라 했는데, `유기체`와 혼동될 수도 있을 것 같음
  - 개발자 뿐만 아니라, 기획자, 디자이너와 함께 시스템을 설계해야 하기 때문에 오히려 구축 시간이 많이 걸릴 수도...
  - 상태 관리와 비즈니스 로직 처리가 애매할 수도 있겠다는 생각이 듬, 페이지 -> 유기체 -> 분자 -> 원자로 `Props`를 계속 전달해야 하는데... 
  - 비슷한 `분자` 컴포넌트가 많이 존재할 수도 있을 것...

  - 📌 참고
  - [리액트와 아토믹 디자인 패턴](https://tech.madup.com/atomic-design/)
    - 매드업의 madTech에서 작성한 글
    - 간단한 예제와 폴더구조 설명
  - [리액트 어플리케이션 구조 - 아토믹 디자인](https://ui.toast.com/weekly-pick/ko_20200213)
    - TOAST UI에서 작성한 글
    - 폴더구조 설명
  - [(우아한테크캠프 3기) Atomic Design Pattern이 뭐지?](https://zoomkoding.github.io/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC%EC%BA%A0%ED%94%84/2020/07/09/atomic-design-pattern.html)
    - 개인 블로그
  - [https://medium.com/@inthewalter/atomic-design-for-react-514660f93ba](https://medium.com/@inthewalter/atomic-design-for-react-514660f93ba)
    - 2019년 부스트캠프 팀프로젝트로 작성한 글
    - https://github.com/connect-foundation/2019-12/ 에서 코드를 볼 수 있음
    - 위의 github에서 아토믹 디자인 패턴 외에 테스팅 코드나 CI/CD 도입기등 흥미로운 글들을 적어 놓음
  - [아토믹 디자인(Atomic Design) 적용기 : 한계점, 단점](https://sumini.dev/guide/009-dont-use-atomic-design/)
    - atomic 디자인의 한계점, 단점을 설명해놓음 
    - 쏘카 프레임, 아틀라시안 디자인시스템의 참고 링크를 걸어놓음
   
### REST API에 대해서 설명해보세요.
3.
4. 
