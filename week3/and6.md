---
### 13장. 스코프
---

**Q. Lexical Environment는 뭘 뜻하는가?**
 - JS 엔진이 현재 읽고 있는 코드의 Scope 혹은 환경을 말한다.
 - 괄호가 있을 때마다 새로운 Lexical Environment가 생성된다.
 - 자신의 Lexical Scope 밖으로 연결해주는 연결고리를 Scope Chain이라 한다.

**Q. 아래 코드를 실행해보고 왜 이리 나왔는지 설명하시오.**
```JS
//입력
var x = 1;
function foo() {
	var x = 10;
	bar();
}
function bar() {
	console.log(x);
}
foo();
bar();

//출력
1
1
```
foo()함수는 bar()을 호출한다. 하지만 bar()함수는 전역변수에 호출되었으며 Lexical Scopre에 의해 foo()함수 안의 지역변수인 10이 아닌 1이 출력된다.

---
### 14장.전역변수의 문제점
---

**Q. 아래 콘솔로그에서 뭐가 나올까? 실행해 봅시다.**
```JS
//입력
var x = 'globaaaaal';
function banana(){
console.log(x); // 여기선 뭐가 나올까??
var x = 'loccccccccccccccccccccccal';
}
banana();
console.log(x);
//출력
undefined
globaaaaal
```

**Q. 전역 객체란 무엇인가?**
 - 전역 범위에 항상 존재하는 객체
 - 최상위에 단 1개만 존재하며 여러 개 만들 수 없다.
 - 전역 객체의 아래에 descendants(자손)으로 위치한다.
 - JS는 소스코드를 실행하기 전에 전역객체를 만든다.

**Q. 아래 키워드로 전역변수 사용 억제법을 찾아보시오.**
 - 1. 즉시 실행 함수(IIFE, Immediately Invoked Function Expression)
   -  정의되자마자 바로 실행하는 함수.
   -  선언과 동시에 호출되어 반환되어 재사용 할 수 없기 떄문에 필요없는 전역 변수의 생성을 줄일 수 있다.
 - 2. 네임 스페이스 객체
      네임스페이스: 개체를 구분할 수 있는 범위.
   -  네임스페이스 객체 자체가 전역 변수에 할당되는 형식이다.
   -  네임스페이스를 분리하여 식별자의 충돌을 방지한다. 이는 외부 라이브러리에 존재하는 함수와 이름이 같을 때도 유용하게 사용되기도 한다.
   -  전역의 네임스페이스 역할을 담당할 객체를 생성한 후 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 식으로 사용한다.
- 3. 모듈 패턴
   - JS의 클로저를 기반으로 동작
   - 특정 부분을 비공개로 유지하여 캡슐화하고 , 외부에서 접근할 수 있는 API를 제공한다. (접근 제한자를 제공하지는 않음.)
- 4. ES6 모듈
   - 사용하면 더 이상 전역 변수를 사용할 수 없음.
   - script태그에 type=”module”어트리뷰트를 추가하여 사용한다.

**Q.전역변수 + 지역변수 관련된 해석을 본인이 직접 최소 30줄 이상의 코드를 작성해서 서술해보시오.**
```JS
var x = 1;
var y = 10;

function foo() {
    var x = 5;
    var y = 55;
    return x + y;
}
function foo2() {
    var x = 2;
    var y = 22;
    return foo()
}
console.log(x) //1
console.log(y) //10
console.log(foo()) //60
console.log(foo2()) //60

function local() {
    var a = 'hello'
}
//console.log(a) //a는 지역변수로 함수밖에서 사용불가

my_name = 'Bb'
//console.log(window.my_name);

function rename() {
    console.log(my_name)
    renaming = "Aa"
}
//console.log(renaming) //renaming이 지역변수 안에는 존재하지만 전역에는 없기에 오류 출력
rename() //변수 선언 시 키워드를 사용하지 않으면 전역 변수로 선언이 되며 console.log(my_name)이 실행될 때 my_name 실행될 때 전역변수로 존재하기 때문이다.
console.log(renaming) //함수호출로 renaming이 전역변수가 됨.
```

---
### 15장. let, const 키워드와 블록 레벨 스코프
---

**Q. 아래 콘솔로그의 결과값을 추론해보시오.**
```JS
var x = 1;
var y = 1;
var x = 100;
var y;
console.log(x);
console.log(y);
//출력
100
1
//변수의 중복 선언이 가능하기에 가장 나중에 선언된 변수의 값을 따른다.
```

**Q. 하단의 코드를 실행하고 에러가 난다면 왜 나는지 설명하시오.**
```JS
let a = 1;
{
	let a = 2;
	let b = 3;
}
console.log(a);
console.log(b);
//출력
1
Uncaught ReferenceError: b is not defined
//let으로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정하여 let b는 지역 변수가 되기 때문이다
```

**Q. 지금까지 했던 코드를 기반으로 let, const  키워드를 적절히 사용하여 var 키워드 대신 써보시오.**
```JS
const x = 1;
const y = 1;
{
	let x = 100;
	let y;

	console.log(x) //100
	console.log(y) //undefined
}
console.log(x); //1
console.log(y); //1
```
