Scope(유효범위)
======
Scope란 유효 범위를 의미하며, **전역 유효범위(global scope)** 와 **지역 유효범위(local scope)** 로 나뉘어진다.

## 함수 단위 유효범위
자바스크립트의 유효 범위는 함수 단위이다.
```js
function outter() {
    function inner() {
        var innerVar = '사과';
        console.log(innerVar); // "사과"
    }
    inner();
    console.log(innerVar); // error : innerVar is not defined
}
outter();
```
inner함수 내에서의 innerVar 접근은 가능하지만,<br>
outter함수에서 innerVar 접근 시 에러가 발생한다.<br>
이를 통해 지역 변수가 가지는 유효 범위는 해당 함수 내라는 것을 알 수 있다.<br>
또한 외장 함수에서 내장 함수의 지역 변수에는 접근이 불가능한 것도 알 수 있다.

```js
function outter() {
    var outterVar = '포도';
    function inner() {
        var innerVar = '사과';
        console.log(innerVar); // "사과"
        console.log(outterVar); // "포도"
    }
    inner();
    console.log(innerVar); // error : innerVar is not defined
    console.log(outterVar); // "포도"
}
outter();
```
하지만 위 예제처럼 내장 함수에서 외장 함수의 지역 변수에 접근은 가능하다.
접근 뿐만아니라 값의 변경또한 가능하다.

### var 키워드의 생략
방금 살펴본 것처럼 내장 함수에서 외장 함수의 변수에 접근이 가능하다는 것을 확인했다.<br>
이 때 내장 함수에서 외장 함수 변수 값을 변경할때 변수의 `var`를 생략한것과 추가한 것의 차이를 알아보자.
```js
function outter() {
    var outterVar = '사과';
    function inner() {
        var outterVar = '포도';
        console.log(outterVar); // "포도"
    }
    inner();
    console.log(outterVar); // "사과"
}
outter();
```
inner함수에서 외장 함수의 변수이름과 동일한 outterVar를 선언하고 다른 값을 넣어보았지만 outter함수의 outterVar의 값은 변경되지 않았다.<br>
이를 통해 자바스크립트에서 변수명은 중복되어 사용이 가능하며,<br>
outter함수의 outterVar와 inner함수의 outterVar는 이름만 동일할 뿐이지 전혀 다른 변수임을 알 수 있다.<br>
그럼 outter함수의 변수의 값을 변경하려면 어떻게 해야 할까?

```js
function outter() {
    var outterVar = '사과';
    function inner() {
        outterVar = '포도';
        console.log(outterVar); // "포도"
    }
    inner();
    console.log(outterVar); // "포도"
}
outter();
```
이전 코드와 차이점은 inner함수에서 outterVar 변수를 선언할 때 `var`키워드를 생략하고 선언하였다.<br>
`var`키워드를 생략한 상태에서 변수를 선언할 경우 자바스크립트에서는 전역으로 변수를 찾은 후 이 값을 변경한다.<br>
따라서 outter함수의 outterVar 변수를 찾은 후 이 값을 갱신한다.<br>
만약 outter함수에 해당 변수가 없을 시 전역 변수를 찾아 이 값을 갱신한다.<br>
만약 해당 변수가 존재하지 않는다면 전역 변수로 새로 선언된다.
>`var`키워드를 생략하고 변수를 선언할 경우 이 변수는 전역 변수의 값을 갱신할 수 있기 떄문에 어떠한 경우에 `var`키워드를 생략해야하는지 정확히 인지한 후에 작성해야 한다.







