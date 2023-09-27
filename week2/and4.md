---
### 11강. 대신 하는 얕은 복사 깊은 복사
---
**Q.밑의 코드를 싱행해보고 이유를 설명해보세요.**
```JS
// <입력문>
const original = {
	[18, 18, 18, 18],
	[19, 19, 19, 19],
	[20, 20, 20, 20],
	[21, 21, 21, 21]
};

const copy = original.slice(); //slice()매소드는 얕은 복사를 한다.

console.log(JSON.stringify(original) === JSON.stringify(copy));

copy[0][0] = 99;
copy[2].push("02");

console.log(JSON.stringify(original) === JSON.stringify(copy));
console.log(original);
console.log(copy);

// <출력문>
true
true
[
  [ 99, 18, 18, 18 ],
  [ 19, 19, 19, 19 ],
  [ 20, 20, 20, 20, '02' ],
  [ 21, 21, 21, 21 ]
]
[
  [ 99, 18, 18, 18 ],
  [ 19, 19, 19, 19 ],
  [ 20, 20, 20, 20, '02' ],
  [ 21, 21, 21, 21 ]
]
```
얕은 복사는 복사된 변수가 원본 객체의 메모리 공간(주소)를 가리키고 있기에 </br>
기존 객체를저장한 변수에 영향을 미친다. -> 복사본의 값을 변경하면 원본의 값 또한 바뀐다.</br></br>

**Q. 밑에 있는 코드들을 실행해 보시고 이유를 생각해 보세요.**
```JS
//입력문
const obj = { a: 1 };
const newObj = Object.assign({}, obj);
newObj.a = 2;
console.log(obj);
console.log(obj === newObj);

//출력문
{ a: 1 }
false
```
assign()은 속성의 값을 복사하는 깊은 복사를 진행하기 때문이다.</br>
console.log(newObj)를 통해 newObj의 값을 확인하면 a: 2임을 볼 수 있다.</br></br>

```JS
//입력값
const obj = {
a: 1,
	b: {
		c: 2,
	},
};
const newObj = Object.assign({}, obj);
newObj.b.c = 3;
console.log(obj);
console.log(obj.b.c === newObj.b.c);
//출력값
{ a: 1, b: { c: 3 } }
true
```
2차원 객체부턴 얕은 복사를 진행하기때문에 obj.b.c와 newObj.b.c는 같은 값으로 판단하며,</br>
2차원 배열 또한 2차원부턴 얕은 복사를 진행한다.</br></br>

**밑에 있는 코드들을 싱행해 보시고 이유를 생각해보세요.**

```JS
//입력값
const obj = {a : 1};
const newObj = Object.assign({}, obj);

newObj.a = 2;

console.log(obj);
console.log(obj === newObj);

//출력값
{ a: 1 }
false
```
1차원 객체를 assign()을 이용해 복사했으므로 깊은 복사를 진행한다.</br></br>
```JS
//입력값
const obj = {
a: 1,
	b: {
		c: 2,
	},
};
const newObj = { ...obj };

newObj.b.c = 3;

console.log(obj);
console.log(obj.b.c === newObj.b.c);

//출력값
{ a: 1, b: { c: 3 } }
true
```
...은 []를 제거해주는 연산자이다. 배열을 합치거나 복사할 때 사용된다.</br>
값을 복사하여 각각의 영역을 수정할 때 사용된다.</br>
...연산자는 깊은 복사를 해주지만 2차원 이상부터는 얕은 복사가 진행되기에 같다고 처리된다.</br>

**Q.아래의 함수를 작동 시켜보세요.**
```JS
//입력문
function deepCopy(obj) {
	if (obj === null || typeof obj !== "object") {
		return obj;
	}
	let copy = {};
	for (let key in obj) {
		copy[key] = deepCopy(obj[key]);
	}
	return copy;
}

const obj = {
	a: 1,
	b: {
		c: 2,
	},
	func: function () {
		return this.a;
	},
};

const newObj = deepCopy(obj);

newObj.b.c = 3;

console.log(obj);
console.log(obj.b.c === newObj.b.c);

//출력문
{ a: 1, b: { c: 2 }, func: [Function: func] }
false
```
deepCopy함수는 깊은 복사를 진행하여 2차원부턴 얕은 복사를 하지만 이 함수를 이용하면 깊은 복사를 사용하여 서로 다르다고 인지한다.</br></br>

**Q. Lodash라이브러리에 대해 조사하고 cloneDeep매서드도 조사해보시오.**
</br>
*lodash*
</br>
JS의 라이브러리이다.</br>
배열 안의 객체들의 값을 핸들링 할 때 유용하며 프론트엔드에 많이 사용된다.</br>
array, collection, date같은 데이터 구조를 간편하게 함수형으로 다룰 수 있게 한다.</br>
native ES6이 lodash보다 더 빠르지만 findIndex()와 map()함수를 통해 객체값을 준다는 점에서 더욱 확장된 함수를 사용할 수 있다는 점에서 생산성이 높다.</br>
</br>
*cloneDeep 매서드*
Lodash에서 사용하는 객체 복사 방법으로 깊은 복사에 사용됩니다.
```JS
//입력문
obj = {
  a: 10,
  b: {
    aa: 'abc'
  }
};

newObj = _.cloneDeep(obj); //깊은 복사로 생성

console.log(obj === newObj)
console.log(obj.a === newObj.a)
console.log(obj.b === newObj.b)
//출력문
false
false
false
```

**Q.소개한 방법 이외에도 깊은복사, 얕은복사 방법을 찾아보세요. 가능하다면 언어 별로 정리해도 좋고, JS만 하셔도 좋고, 단일 언아 하나만 하셔도 됩니다.**
</br>
*Python*
```Python
# shallow copy(얕은 복사)
a=[1,2,3]
b=a[:] # b=a.copy()도 똑같이 동작
b.append(1)
print(f"{a=}, {b=}")
print(f"{id(a)=}, {id(b)=}")
# 출력 값을 보면 b에 1만 추가되고 a는 그대로있으며 변수가 가리키는 메모리 주소가 서로 달라졌기 때문이다.
# 얕은 복사로는 변수간 독립성이 보장되지 않는다.
# 중첩 리스트나 중첩 딕셔너리 등 복잡한 구조를 가지는 mutable변수에선 한계가 나타난다.

#deep copy(깊은 복사)
import copy
a=[[1,2],[3,4]]
b = copy.deepcopy(a)
a[0][0]=100
print(f"{a=}, {b=}")
print(f"{id(a)=}, {id(b)=}")
print(f"{id(a[0])=}, {id(b[0])=}")
# 출력 값을 보면 b[0][0]은 변경되지 않고 메모리 주소도 다른 것을 통해 독립성이 유지된다는 것을 알 수 있다.
```
