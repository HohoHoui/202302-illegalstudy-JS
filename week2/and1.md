---
### 9장. 타입 변환과 단축 평가
---
**그렇다면 암묵적인 타입 변환(타입 강제 변환)이 무조건적으로 좋지 않은 문화이자 기능인가?**

예상치 못한 타입을 받았을 떄 예상 가능한 타입으로 바꿈으로써 사용자의 실수를 바로잡아 에러를 예방할 수 있는 장점이 있다.
</div>

---
### 9장. 단축 평가(심화)
---
**아래 설명에 따라 단축 평가를 이용하여 아래의 if문처럼 작동하는 ture값 여부를 판별하는 코드를 빈칸에 알맞게 작성해보시오.**

**결과도 내시길 바랍니다.(빈칸의 길이와 정답의 길이가 상이할 수 있습니다.)**

```JS
//<입력>
var isThereMessage = true;
var message = '';

if(isThereMessage) massage = '멘토는 죽어있다.';
message = false || message;
console.log(message);
//<출력>
//멘토는 죽어있다.
```

---
### 10장. 객체 리터럴
---
**아래의 코드를 시행해보식 왜 결과 값이 그렇게 나오는지 생각해보세요.**

```JS
var person = {
	firstName : 'turtle',
	last-name : 'park'
};
console.log(person); //SyntaxError: Unexpected token '-' -는 객체의 키값(프로퍼티 명)에 쓰일 수 없다.
-------------------------
var word1 = {
	var : '',
	function: ''
};
console.log(word1); //{var: '', function: ''} 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성되기 때문이다.
----------------------
//프러퍼티 키 동적 생성
var objES5 = {}
var keyES5 = 'ES5'
objES5[keyES5] = 'world';

console.log(objES5); //{ES5: 'world'} 
//ES6이후부터 동적으로 키를 생성할 수 있게 되었으며  대괄호 접근자를 이용하여 사용한다.
//객체에 존재하지 않는 프로퍼티를 참조하여 값을 할당하면 해당 프로퍼티가 동적으로 생성됨.
//대괄호를 이용하여 프로퍼티 키를 동적으로 생성할 수 있다.
----------------------
//계산된 프로퍼티 이름
var keyES6 = 'HELL';
var objES6 = {[keyES6]: 'o'};

console.log(objES6); //{HELL: 'o'}
//계산된 프로퍼티: 객체 리터럴 안의 프로퍼티 키가 대괄호로 둘러싸여 있는 것으로 객체의 변수명에 미리 계산된 변수를 넣는 것이 가능하다.
-----------------------
var emptyObj = {
	'' : ''
};
console.log(emptyObj); //{"": ''}
// 중괄호 내에 프로퍼티를 정의하지 않거나 빈 상대로 두면 빈 객체가 생성된다.
-----------------------
var numObj = {
1 : 0,
2 : 1,
3 : 2
};
console.log(numObj); //{1: 0, 2: 1, 3: 2}
// key에는 빈 문자열을 포함한 모든 문자열 또는 symbol값이 들어갈 수 있다.
// 문자열이나 symbol 이외의 값을 지정하면 암묵적으로 타입이 변환되어 문자열이 된다.
-----------------------
var duplicateObj = {
	name : 'park',
	name : 'kim'
};
console.log(duplicateObj);
//이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.
```

**브라우저 화경과 Node.js환경을 준비히고 아래의 코드를 돌려보시오.**
```JS
var wind = {
	'last-name' : 'park',
	1: 10
};

wind.'last-name'; //SyntaxError: Unexpected string
wind.last-name; //ReferenceError: name is not defined

wind[last-name]; //ReferenceError: last is not defined
wind['last-name']; //Park
wind.1; //SyntaxError: Unexpected number
wind.'1'; //SyntaxError: Unexpected String
wind[1]; //10
wind['1']; //10
```
---
### 추가과제.1
---

**반복문과 조건문을 이용한 프로그램 만들기.(입력값, 코드 업로드)**

**forif이용해서 하기.**


---
### 추가과제.2
---
**단축평가에 대해 한번 예제 코드를 제외하고 코딩을 한번 시도해보시오.**

**해당 단어나 기타 로직에 대해 뜻같은 거 다 조사해도 상관없음.**
```JS
//1. 서버 사용을 위해 http모듈을 http변수에 담음.(모듈과 변수의 이름은 달라도 됨)
var http = require('http');

//2. http 모듈로 서버를 생성.
//서버를 생성한 후, 사용자로부터 http요청이 들어오면 function 블럭내부의 코드를 실행하여 응답한다.
var server = http.createServer(function (request, response) { //request, response부분은 요청, 응답으로 한국어로 할 수도 있음.

    response.writeHead(200, { 'Content-Type': 'text/html' }); //{}안은 키 : 값 형태 200 : 웹서버에 들어오는 요청에 대한 정상적으로 값을 리턴해주는 것
    //서버 측에서 보내주는 컨텐츠의 타입이 텍스트이고, html 형태임을 알려줌
    response.end('Hello hode.js!!'); //실제 코드 값을 end()함수로 전달하면 브라우저는 해당 컨텐츠를 받은 후 html을 해석하여 화면에 출력

});

//3. listen 함수로 8080포트를 가진 서버를 실행. 서버가 실행된 것을 콘솔창에서 확인하기 위한 로그 출력
server.listen(8080, function () { //서버 시작
    //console.log('Server is running...');
});

//https://plan2018.tistory.com/892

const readline = require("readline"); //모듈 가져오기

const rl = readline.createInterface({ //readline모듈을 이용해 입출력을 위한 인터페이스 객체 생성
    input: process.stdin,
    output: process.stdout,
});

var answer;
var isHungry = answer;
var hungry = '';

rl.question("배가 고픈가요?(true or false)", (answer) => { //r변수 생성
    if (answer == 'true') hungry = '배가 고프다.';
    if (answer == 'false') hungry = '배가 안고프다.';
    else hungry = '입력값이 true또는 false가 아닙니다.'
    hungry = false || hungry;
    console.log(hungry);
    rl.close();
});

rl.on('close', () => { //입력이 끝난 후 실행코드
    process.exit();
})
```
**<출력결과>**
</div>
![image](https://github.com/HohoHoui/202302-illegalstudy-JS/assets/97030768/3a7efd6e-e91d-4d05-9704-16996fb9fc96)
