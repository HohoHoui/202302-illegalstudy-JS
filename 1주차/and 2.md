***
# 5장
***
### 과제5_1번. 아래의 코드에서 표현식인 부분과 표현식이 아닌 부분에 대해 구분하시오.
```JS
var x; // 변수를 선언하는 선언문이다
x = 100; //값을 할당하는 표현식인 동시에 완전한 문이므로 표현식 문이다.

var a = y = 100; //선언과 동시에 할당을 하기에 표현식 문이다.
console.log(a); //console.log(a)는 값으로 사용 가능하기에 표현식이다.

var foo = var x; //표혐식이 아닌 문은 값처럼 사용할 수 없다.
```

***
# 6장
***
### 과제6_1번. 그렇다면 위에 설명과 같이 다 실수로 측정한다면 2진수, 8진수, 16진수를 출력하면 어떤 식으로 될까?
입력문
```JS
var binary = 0b01000001;
var octal = 0o101;
var hex = 0x41;

console.log(binary, octal, hex);
if(binary === hex) console.log(true);
if(binary === octal) console.log(true);
````

출력문
```JS
65 65 65 //2진수 8진수 16진수 모두 상관하지 않고 모두 같은 타입으로 판단한다.
true
true
```

### 과제6_2번. 다  실수라고 하면 아래의 비교문의 결과는 어떻게 나올까?
입력문
```JS
console.log(1 === 1.0); //true
console.log(4 / 2); //2
console.log(3 / 2); //1.5
```
출력문
```JS
true
2
1.5
```

### 과제6_3번. 위에 세 가지를 console을 이용하여 도출하여 보시오.
1. infinity  : 양의 무한대
2. -infinity : 음의 무한대
3. NaN(Not A Number) : 산술 연산 불가

입력문
```JS
console.log(Infinity + Infinity);
console.log(-Infinity + -Infinity);
console.log(Infinity + -Infinity);
```
### 과제6_4번. 만약 NaN이 아닌 nan, NAN같이 변수에 대입하면 어떤 식으로 나올까요?
nan과 NAN은 정의된 것이 아니기 때문에 레퍼런스 에러가 나온다.

### 과제6_5번.  “”안의 ‘’(single quote)은 뭘로 인식되고 ‘’(single quote) 안의 “”은 뭘로 인식될까?
입력문
```JS
var a = "이거랑'이거랑'";
var b = '꽃게랑"꽃게랑"';
console.log(a);
console.log(b);
```

출력문
```JS
이거랑'이거랑' //character(문)와 같은 것으로 인식된다.
꽃게랑"꽃게랑"
```

### 과제6_6번. 그렇다면 아래의 코드는 어떤식으로 다를까?
입력문
```JS
console.log(`a + b = ${1 + 2}`);
console.log('a + b = ${1 + 2}');
```

출력문
```JS
a + b = 3 //백틱 안의 ${}안은 수식은 연산이 가능하다.
a + b = ${1 + 2} //모두 문자로 인식한다.
```

### 과제6_7번. 의도적인 부재를 왜 사용하는가?
의도적인 부재 : null을 변수에 값이 없다는 것을 의도적으로 명시할 때 사용.
- 변수 초기화를 하며 의도적으로 값을 설정하지 않고자 할 때 null을 사용.
- 객체의 특정 속성이 없음을 명시적으로 표시하고자 할 때 사용.
-> js에서 의도적으로 값을 부재하게 만들고 싶을 때 사용.

### 과제6_8번. 과연 아래의 사용법이 옳은 선택인가? 다른 방법으로 변수를 소멸시키는 게 좋지 않을까?
예제
```JS
var night = 'Turtle';
night = null;
```
**방법**
즉시 실행 :굳이 전역변수를 사용할 이유가 없다면 지역 변수 사용을 애용하기.
네임 스페이스 객체 : 전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법.
모듈 패턴: 클래스를 모방해서 관련이 있는 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈로 만드는 것. 클로저 제공.

### 과제6_9번. ECMAScript 사양은 문자열과 숫자 타입들 외에는 명시적으로 규정하고 있지 않은데 그렇다면 해당 데이터 타입들은 어떤 식으로 계산되고 있는가?

**Undefined**
var를 써서 변수를 정의했지만 초기화하지 않은 경우 undefined를 할당. 
생성하지 않은 변수에 대해 typeof 연산자를 사용할 경우 undefoned를 할당한다.
(→ 선언 후 값을 할당하지 않으면 자동으로 할당되는 원시값.)

**null**
값을 하나만 가짐. 
빈 객체를 가리키는 포인터로 null에 typeof를 호출하면 object를 반환한다.
(→ 비어있는 값이라는 것을 명시적으로 사용할 때 쓰는 윈시값.)

**Boolean**
true, false 두가지 리터럴 값을 가지는 데이터 타입이다.
EMACScript에선 모든 타입을 Boolean()함수를 사용하여 모든 타입을 불리언값으로 표현할 수 있다.

**Symbol**
ES6에서 추가된 7번째 타입.
외부에 노출되지 않고 다른 값과 중복되지 않는 유일한 값.
충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용.
Symbol 함수를 호출하려 생성한다.

**객체**
ECMAScript에서 객체는 데이터와 기능의 집합이다.

### 과제6_10번. 심벌 테이블 이라는 뜻을 알아보시오.
테이블: 행과 열로 짜여진 표에 기록된 데이터의 집합.
심벌 테이블 : 컴파일러 또는 인터프리터 같은 언어 변환기에서 사용되는 데이터 구조.
js에서의 심벌 테이블 : 특정 심볼을 꺼내쓰기 위해 전역 심볼 테이블이 존재한다.

### 과제6_11번. 대표적인 동적/정적 언어를 조사해보시오.( == 강/약 타입 언어)
**정적 언어**
컴파일 시 변수 타입이 결정되는 언어로 작성자가 소스 코드를 보고 변수 타입을 직접 작성하는 언어이다. 
- c, c++, c#, java, Scala, Fortran, Haskell, ML, Pascal

**동적 타입 언어**
런타임시 변수의 타입이 결정되는 언어로  코드를 실행할 때 알아서 변수 타입을 판단해주는 언어이다.
- JavaScript, Ruby, Python, PHP, Smalltalk, Lisp, Groovy

***
# 7장
***

### 7_1번. 아래의 코드를 실행해 보자.
입력문
```JS
var a = '1';
console.log(+a, typeof +a);
console.log(a, typeof a);
a = true;
console.log(+a, typeof +a);
console.log(a, typeof a);
a = false;
console.log(+a, typeof +a);
console.log(a, typeof a);
a = 'Hi';
console.log(+a, typeof +a);
console.log(a, typeof a);
```

출력문
```JS
1 'number'
1 string
1 'number'
true 'boolean'
0 'number'
false 'boolean'
NaN 'number'
Hi string
```

### 과제7_2번. 암묵적 타입 변환 또는 타입 강제 변환에 대해 알아보시오.
변수 값을 재할당해서 변경하는 것이 아닌 자바스크립트 엔진이 표현식을 에러없이 평가하기 위해 기존 값을 바탕으로 새로운 타입의 값을 만들어 단 한번 사용하고 버리는 것.
문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환한다.
자바스크립트 엔진에 의해 암묵적으로, 즉 드러나지 않게 타입이 자동 변환되기 때문에 타입을 변경하겠다는 개발자의 의지가 코드에 명확히 드러나지 않는다.

### 과제7_3번. 아래의 비교가 뭐가 다른지 알아오시오.
```JS
//입력
5 == 5; //true -> 숫자와 숫자가 같은지를 판단하기에 참을 출력.
5 == '5'; //true -> 숫자형인 5와 문자형인 5가 같은지 다른지 비교한 것이며 값은 둘 다 5기에 참을 출력

5 === 5; //true
5 === '5'; //false -> 둘의 데이터 타입이 다르기 떄문에 2번째의 경우 거짓을 출력

'0' == ''; //fasle -> 0이라는 문자가 들어있는 '0'과 속이 빈 ''를 비교하는 것이기 때문이다.()
0 == ''; //true -> '' : 안에 값을 가질 수 있는 참조형 타입이고 0은 숫자형 타입이다. 참조형 타입을 워시형 타입으로 뱐환하여 안이 빈 ''은 0이 된다. 고로 참이 출력된다.
0 == '0'; //true -> 숫자 타입과 문자 타입의 비교로 문자 타입이 숫자 타입으로 변환된다. 고로 참을 출력한다.

//js는 비교하기 전 피연산자의 타입이 다르면 동일한 타입으로 변환시킨다.
//숫자와 문자를 비교할 경우, 문자열을 숫자로 변환한다.
//하나의 피연산자가 참조형 데이터 타입이고 다른 하나가 문자열이나 숫자 타입이면, 피연산자를 valueOf()나 toString()을 사용해 원시형 타입으로 변환한다.

false == 'false'; //fasle ->false의 타입은 불린으로 toNumber(x) == y가 된다. 여기서 false는 숫자로 전환되어 +0이 되어 +0 == 'false'가 된다. 여기서 숫자와 문자를 비교하게 되며 문자는 NaN으로 전환된다. 고로 거짓을 출력한다.
false == '0'; // true -> '0'은 거짓으로 판단하기에 false == false가 되며 참을 반환한다.
false == null; // false -> 불린 타입은 ToNumber을 거쳐 숫자가 된다. 이때 true는 1, false는 +0이 된다. null은 1 또는 +0과 타입이 달라 비교할 수 없다. 그렇기에 거짓을 출력한
false == undefined; // false -> 위의 이유와 비슷한 이유이다.

NaN === NaN //false -> js의 오류이다. (IEEE754부동 소수점 관련. NaN은 절대 같지 않다) https://stackoverflow.com/questions/19955898/why-is-nan-nan-false
0 == -0 //true -> (strict equality comparison algorithm)정적 균등 비교 알고리즘(?)을 사용하며 type()의 동작할 때 -0과 0을 비교하면 true를 출력한다.
0 === -0 //true -> 위의 이유와 같음.
```

### 과제7_4번. 아래의 결과가 다른 이유를 설명하시오.
```JS
-0 === 0; //true
Object.is(-0.0); //false

NaN === NaN; //true
Object.is(NaN, NaN); //false
// Object.is()함수는 두 수가 같은 지 다른 지 판단하지만 ==나 ===와도 차이가 있다.
// 부호있는 0과 NaN 값들의 처리를 ===와 다르게 하는데 +0과 -0을 다르게 처리하며 NaN을 서로 같지 않게 처리한다.
// 그렇기에 위의 ===연산은 둘 다 참이 나왔지만 Object.is()는 거짓이 출력된 것이다.
```

### 과제7_5번. 위에 있는 반환 값을 다 나타내보시오.
```JS
typeof // 피연산자의 데이터 타입을 문자열로 반환.
typeof 1; //number
typeof 'a'; // string
typeof true; // boolean
typeof a; //undefined

const A = Symbol('hi');
typeof A; //symbol

typeof []; //object
typeof Object.is; //function
```
***
# 8장
***
### 과제8_1번. 백준 문제를 js를 이용해 풀기
fs모듈 방법으로 진행
js는 화이트스페이스(공백, 줄바꿈)로 잘라서 하나씩 받아오는 기능이 없다. 
→ split 메서드를 사용.
→vscode로 js를 쓰기 위해선 node.js를 설치해야 한다.
→ vscode에서 코드를 실행하기 위해선 확장 플러그인인 Code Runner를 설치해야.

**백준 10871번**
index.js코드
```JS
const fs = require("fs");
const path = process.platform === 'linux' ? '/dev/stdin' : './example.txt';
let input = fs.readFileSync(path).toString().split('\n');

const [inputN, inputX] = input[0].split(' ').map((item) => +item);
const arrA = input[1].split(' ').map((item) => +item);

solution(inputN, inputX, arrA);

function solution(N, X, arrA) {
    const correctA = [];

    for (let count = 0; count != N; count++) {
        if (arrA[count] < X) {
            correctA.push(arrA[count]);
        }
    }

    console.log(correctA.join(' ')); //정답 출력
}
```

example.txt코드(?)
10 5
1 10 4 9 2 3 8 5 7 6

문제풀이 화면 
