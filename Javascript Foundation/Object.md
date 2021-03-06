객체의 생성과 접근
======
객체를 생성하는 방법과 객체의 속성에 접근하는 방법

## 객체 생성
객체를 생성하는 방법에는 생성자 함수를 이용한 방법과 객체 리터럴 방식을 이용할 수 있다.

### 생성자 함수를 이용한 객체 생성
자바스크립트 내장 함수인 Object() 생성자 함수를 이용해 객체를 생성하는 방법이다.
변수를 선언 후 Object함수 앞에 **new**키워드를 붙여준다.

```js
var emptyObj = new Object();
```
### 객체 리터럴 방식을 이용한 객체 생성
생성자 함수를 사용한 방법 말고도 간단하게 객체를 생성할 수 있는 객체 리터럴 방식이다.
변수를 선언 후 중괄호를 넣어준다.

```js
var emptyObj = {};
```
### 객체의 프로퍼티
객체를 생성했다면 그 안의 내용물들을 채워넣을 차례이다.
객체를 구성하는 요소를 **프로퍼티** 라고하며 프로퍼티의 구성은 '이름(key)' : '값(value)'로 되어있다.<br>
프로퍼티의 값으로는 객체,변수,함수 등 모든 것들을 포함할 수 있으며,
프로퍼티의 값으로 함수가 오게될 경우 이를 **메서드**라고 부른다.
#### 프로퍼티의 생성
```js
// 객체 리터럴을 통한 person객체 생성
var person = {
    name : 'hongsun',  // 이름(key) : 'name' , 값(value) : 'hongsun'이된다
    age : 27
};
```
위 처럼 최초 객체를 생성시에 프로퍼티를 함께 생성할 수도 있지만 이미 생성되어 있는 객체에 프로퍼티를 추가할 수도 있다.
```js
// 빈 객체 생성
var emptyPerson = {};
emptyPerson.name = 'hongsun';
emptyPerson.age = 27;
console.log(emptyPerson) // {name:"hongsun", age: 27}
```
#### 프로퍼티의 접근
위의 예제처럼 객체를 생성, 접근할때 사용되는 연산자는 두가지가 있다.

* 마침표(.)표기법
* 대괄호([])표기법

두 표기법의 사용법과 차이는 아래와 같다
```js
var obj = {
    nickName : 'pubho',
    'full-name' : 'ahn hong sun'
};
console.log(obj.nickName, obj['nickName']); // "pubho", "pubho"
console.log.(obj.full-name, obj['full-name']) // NaN, "ahn hong sun"
```
일반적인 경우에는 마침표 표기법을 사용하면 되지만 주의할 것은 대괄효 표기법을 언제 사용하느냐이다.<br>
대괄호 표기법을 사용해야하는 경우는 접근하려는 프로퍼티 이름이 표현식이거나 예약어일 경우이다.<br>
위 예제의 'full-name' 은 '-'연산자를 가지고 있는 표현식이기 때문에 대괄호 안에 따옴표를 넣어 문자열로 변환 후 접근해야 한다.
따옴표를 사용해 문자열로 전환하지 않고 접근 시에는 full과 name간의 '-'연산이 되므로 NaN을 반환하며 에러를 발생하게 된다.

>**NaN (Not a Number)**<br>
자바스크립트에서 NaN값이 반환될 경우는 수치 연산을 해서 정상적인 값을 얻지 못할 경우에 반환된다.<br>

#### for in 문을 통한 객체의 프로퍼티 순회 및 출력
for in 문을 사용하면 객체의 모든 프로퍼티를 출력할 수 있다.
```js
var obj = {
    name : 'pubho',
    age : 27,
    hobby : 'fishing'
};

// 프로퍼티의 값을 담을 빈 변수인 key 선언(생략가능하다)
var key;
// 객체의 프로퍼티를 하나씩 순회하며 key 변수에 프로퍼티의 이름을 담아 프로퍼티 값들을 출력하고 있다.
for (key in obj) {
    console.log('이름(key): ' + key +' , ', '값(value): ' + obj[key] )
} 
// 출력 결과
이름(key): name ,  값(value): pubho
이름(key): age ,  값(value): 27
이름(key): hobby ,  값(value): fishing
```

#### 프로퍼티 삭제
delete 연산자를 이용해 객체의 프로퍼티를 삭제할 수 있다.<br>
하지만 **객체 자체를 삭제할 수는 없다**.
```js
var obj = {
    name : 'pubho',
    age : 27
};
console.log(obj.name); // pubho
delete obj.name;
console.log(obj.name); // undefined

delete obj; // 객체 삭제 시도
console.log(obj.age); // 27을 반환, 객체는 삭제되지 않는다는걸 확인할 수 있음
```
>자바스크립트는 존재하지 않는 프로퍼티에 접근할 경우 에러를 반환하는 것이아니라 undefined를 반환한다.<br>
따라서 위 예제에서 obj.name 프로퍼티는 삭제된 것을 확인 할 수있다.