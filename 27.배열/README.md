# 27장 배열

## 목차

- [배열이란 ?](#27.1)
- [자바스크립트 배열은 배열이 아니다](#27.2)
- [length 프로퍼티와 희소 배열](#27.3)
- [배열 생성](#27.4)
- [배열 요소의 참조](#27.5)
- [배열 요소의 추가와 갱신](#27.6)
- [배열 요소의 삭제](#27.7)
- [배열 메서드](#27.8)
- [배열 고차 함수](#27.9)

## 27.1 배열이란 ? <a name= "27.1"></a>

- `배열`은 여러 개의 값을 순차적으로 나열한 자료구조다.
- 자바스크립트의 모든 값은 배열의 요소가 될 수 있다. 즉, 원시값은 물론 객체, 함수, 배열 등 자바스크립트에서 값으로 인정하는 모든 것은 `배열`의 요소가 될 수 있다.
- `배열`의 길이를 나타내는 length 프로퍼티를 갖는다.
- 자바스크립트에 `배열`이라는 타입은 존재하지 않는다. `배열`은 객체 타입이다.
- 배열과 객체의 특징 비교
  | 구분 | 객체 | 배열 |
  | ------------- | ----------------- | ------------- |
  | 구조 | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
  | 값의 참조 | 프로퍼티 키 | 인덱스 |
  | 값의 순서 | ✕ | ○ |
  | length 프로퍼티 | ✕ | ○ |


## 27.2 자바스크립트 배열은 배열이 아니다 <a name= "27.2"></a>

- 자료구조에서 말하는 `배열`은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다. 즉, `배열`의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 `배열`을 `밀집 배열`이라 한다.
- 자바스크립트의 `배열`은 자료구조에서 말하는 일반적인 의미의 `배열`과 다르다. 즉 `배열`의 요소를 위한 각각의 메모리 공간은 동리한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수 도 있다. `배열`의 요소가 연속적으로 이어져 있지 않는 `배열`을 `희소 배열`이라 한다
- 자바스크립트의 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체다.
- 일반적인 `배열`과 자바스크립트 `배열`의 장단점
  - 일반적인 `배열`은 인덱스로 요소에 빠르게 접근할 수 있다. 하지만 요소를 삽입 또는 삭제하는 경우에는 효율적이지 않다.
  - 자바스크립트 `배열`은 해시 테이블로 구현된 객체이므로 인덱스로 요소에 접근하는 경우 일반적인 `배열`보다 성능적인 면에서 느릴수밖에 없는 구조적인 단점이 있다. 하지만 요소를 삽입 또는 삭제하는 경우에는 일반적인 `배열`보다 빠른 성능을 기대할 수 있다.


## 27.3 length 프로퍼티와 희소 배열 <a name= "27.3"></a>

- length 프로퍼티는 요소의 개수, 즉 `배열`의 길이를 나타내는 0 이상의 정수를 값으로 갖는다.
- length 프로퍼티의 값은 빈 `배열`의 경우 0이며, 빈 `배열`이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.
- length 프로퍼티의 값은 0과 2<sup>32 미만의 양의 정수다. 즉, `배열`은 요소를 최대 2<sup>32 - 1(4,294,967,295)개 가질 수 있다.
- length 프로퍼티의 값은 `배열`에 요소를 추가하거나 삭제하면 자동 갱신된다.
- length 프로퍼티 값은 요소의 개수, 즉 `배열`의 길이를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.
  - 현재 length 프로퍼티 값보다 작은 숫자 값을 할당하면 `배열`의 길이가 줄어듬
  - 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우 length 프로퍼티 값은 변경되지만 실제로 `배열`의 길이가 늘어나지는 않는다
- 희소 `배열`은 length와 `배열` 요소의 개수가 일치하지 않는다. `희소 배열`의 length는 `희소 배열`의 실제 요소 개수보다 언제나 크다.

## 27.4 배열 생성 <a name= "27.4"></a>

- 객체와 마찬가지로 `배열`도 다양한 생성 방식이 있다.
- 가장 일반적이고 간편한 `배열` 생성 방식은 `배열` 리터럴을 사용하는 것이다.

#### 27.4.1 배열 리터럴

- `배열` 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호([])로 묶는다.
- `배열` 리터럴은 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.

```js
const arr = [];
```

```js
const arr = [1, 2, 3];
```

```js
const arr = [1, , 3]; // 요소 생략 시 희소 배열
```

#### 27.4.2 Array 생성자 함수

- Array 생성자 함수를 통해 `배열`을 생성할 수 있다.
- Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작한다.
- `배열`은 최대 2<sup>32 - 1(4,294,967,295)개 가질 수 있다
- 전달된 인수가 음수이면 에러가 발생한다.

전달된 인수가 1개이고 숫자인 경우 length 프로퍼티 값이 인수인 `배열`을 생성

```js
const arr = new Array(10);
console.log(arr); // [empt x 10]
console.log(arr.length); // 10
// 이 때 생성된 배열의 요소는 존재하지 않고 length 프로퍼티의 값도 0이 아니므로 희소 배열이다.
```

전달된 인수가 없는 경우 빈 `배열`을 생성

```js
new Array(); // []
```

전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 `배열` 생성

```js
new Array(1, 2, 3); // [1, 2, 3]

new Array({}); // [{}]
```

#### 27.4.3 Array.of

- ES6에서 도입된 메서드로 전달된 인수를 요소로 갖는 `배열`을 생성한다.
- Array 생성자 함수와 다르게 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 `배열`을 생성한다.

```js
Array.of(1); // [1]

Array.of(1, 2, 3); // [1 ,2 ,3];

Array.of('string'); // ['string']
```

#### 27.4.4 Array.from

- ES6에 도입된 메서드로 유사 `배열` 객체 또는 이터러블 객체를 인수로 전달받아 `배열`로 변환하여 반환한다.

```js
Array.from({ length: 2, 0: 'a', 1: 'b' }); // ['a', 'b']

Array.from('Hello'); // ['H', 'e', 'l', 'l', 'o']
```

- 두 번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다.

```js
Array.from({ length: 3 }); // [undefined, undefined, undefined]

Array.from({ length: 3 }, (_, i) => i); // [0, 1, 2]
```

## 27.5 배열 요소의 참조 <a name= "27.5"></a>

- `배열`의 요소를 참조할 때는 대괄호([]) 표기법을 사용한다.
- 정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다.
- 인덱스는 값을 참조할 수 있다는 의미에서 객체의 프로퍼티 키와 같은 역할을 한다.

## 27.6 배열 요소의 추가와 갱신 <a name= "27.6"></a>

- 객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 `배열`에도 요소를 동적으로 추가할 수 있다.
- 존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다.
- 이때 length 프로퍼티 값은 자동 갱신된다.

```js
const arr = [0];

arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2
```

현재 `배열`의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 `희소 배열`이 된다.

```js
arr[100] = 100;

console.log(arr); // [0, 1, empty x 98, 100]
console.log(arr.length); // 101
```

인덱스는 요소의 위치를 나타내므로 반드시 0이상의 정수(또는 정수 형태의 문자열)를 사용해야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다.

```js
const arr = [];

arr[0] = 1;
arr['1'] = 2;
arr['foo'] = 3;
arr.bar = 5;
arr[-1] = 6;

console.log(arr); // [1, 2, foo: 3, bar: 5, -1: 6]
console.log(arr.length); / 2
```

## 27.7 배열 요소의 삭제 <a name= "27.7"></a>

- `배열`은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 delete 연산자를 사용할 수 있다.
- delete 연산자는 객체의 프로퍼티를 삭제한다.
- 이 때 `배열`은 `희소 배열`이 되며 length 프로퍼티 값은 변하지 않는다. 따라서 `희소 배열`을 만드는 delete 연산자는 사용하지 않는 것이좋다.
- `희소 배열`을 만들지 않으면서 `배열`의 특정 요소를 완전히 삭제하려면 Array.prototype.splice 메서드를 사용한다.

## 27.8 배열 메서드 <a name= "27.8"></a>

- `배열` 메서드는 결과물을 반환하는 패턴이 아래 두가지가 있다.
- `원본 배열`(배열 메서드를 호출한 배열, 즉 배열 메서드의 구현체 내부에서 this가 가리키는 객체)을 직접 변경하는 메서드
- `원본 배열`을 변경하지 않고 새로운 배열을 반환하는 메서드가 있다.
- `원본 배열`을 변경하는 메서드는 외부 상태를 변경하는 부수 효과가 있으므로 사용할 때 주의해야 한다 따라서 가급적 `원본 배열`을 직접 변경하지 않는 메서드를 사용하는 편이 좋다.

#### 27.8.1 `Array.isArray`

- Array 생성자 함수의 정적 메서드 (Array.of, Array.from 도 정적 메서드)
- Array.isArray 메서드는 전달된 인수가 `배열`이면 true, `배열`이 아니면 false를 반환한다.

```js
// true
Array.isArray([]);
Array.isArray(new Array());

// false
Array.isArray({});
Array.isArray(null);
```

#### 27.8.2 `Array.prototype.indexOf`

- indexOf 메서드는 `원본 배열`에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.
  - 중복 요소가 여러 개 있으면 첫번째 요소 반환
  - 요소가 존재하지 않으면 -1 반환
  - 두 번째 인수는 검색을 시작할 인덱스. 두 번째 인수를 생략하면 처음부터 검색

```js
const arr = [1, 2, 2, 3];

arr.indexOf(2); // 1

arr.indexOf(4); // -1

arr.indexOf(2, 2); // 2
```

- indexOf 메서드 대신 ES7에 도입된 `Array.prototype.includes` 메서드를 사용하면 가독성이 더 좋다.

```js
const foods = ['apple', 'banana'];

if (!foods.includes('orange')) {
  foods.push('orange');
}
console.log(foods); // ['apple', 'banana', 'orange']
```

#### 27.8.3 `Array.prototype.push`

- push 메서드는 인수로 전달받은 모든 값을 `원본 배열`의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.
- push 메서드는 `원본 배열`을 직접 변경한다.

```js
const arr = [1, 2];

let result = arr.push(3, 4);
console.log(result); // 4

console.log(arr); // [1, 2, 3, 4];
```

- push 메서드는 성능면에서 좋지 않다. 마지막 요소로 추가할 요소가 하나뿐이라면 length 프로퍼티를 사용하여 마지막 요소에 직접 추가 하는 것이 push 메서드 보다 빠르다.
- push 메서드는 `원본 배열`을 직접 변경하는 부수 효과가 있기 떄문에 ES6의 스프레드 문법을 사용하는 편이 좋다.
- 스프레드 문법을 사용하면 함수 호출 없이 표현식으로 마지막에 요소를 추가할 수 있으며 부수 효과도 없다.

```js
const arr = [1, 2];

const newArr = [...arr, 3];
console.log(newArr); // [1, 2, 3]
```

#### 27.8.4 `Array.prototype.pop`

- pop 메서드는 `원본 배열`에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
- `원본 배열`이 `빈 배열`이면 undefined를 반환한다.
- pop 메서드는 `원본 배열`을 직접 변경한다.

```js
const arr = [1, 2];

let result = arr.pop();
console.log(result); // 2

// pop 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

#### 27.8.5 `Array.prototype.unshift`

- unshift 메서드는 인수로 전달받은 모든 값을 `원본 배열`의 앞에 추가하고 변경된 length 프로퍼티 값을 반환한다.
- unshift 메서드는 `원본 배열`을 직접 변경한다.

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);
console.log(result); // 4

// unshift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 4, 1, 2]
```

- unshift 메서드는 `원본 배열`을 변경하는 부수 효과가 있기 때문에 ES6의 스프레드 문법을 사용하는 편이 좋다.
- 스프레드 문법을 사용하면 함수 호출 없이 표현식으로 앞에 요소를 추가할 수 있으며 부수 효과도 없다.

```js
const arr = [1, 2];

const newArr = [3, 4, ...arr];
console.log(newArr); // [3, 4, 1, 2]
```

#### 27.8.6 `Array.prototype.shift`

- shift 메서드는 `원본 배열`에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
- `원본 배열`이 `빈 배열`이면 undefined를 반환한다.
- shift 메서드는 `원본 배열`을 직접 변경한다.

```js
const arr = [1, 2];

// 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.shift();
console.log(result); // 1

console.log(arr); // [2];
```

#### 27.8.7 `Array.prototype.concat`

- concat 메서드는 인수로 전달된 값들(배열 또는 원시값)을 `원본 배열`의 마지막 요소로 추가한 `새로운 배열`을 반환한다.
- 인수로 전달한 값이 `배열`인 경우 해체하여 `새로운 배열`의 요소로 추가한다.
- `원본 배열`은 변경되지 않는다.

```js
const arr1 = [1, 2];
const arr2 = [3, 4];
let result = arr.concat(arr2);
console.log(result); // [1, 2, 3, 4]

result = arr1.concat(3);
console.log(result); // [1, 2, 3]

result = arr1.concat(arr2, 5);
console.log(result); // [1, 2, 3, 4, 5]

console.log(arr1); // [1, 2]
```

- concat 메서드는 ES6의 스프레드 문법으로 대체할 수 있다.

```js
const arr1 = [1, 2];
const arr2 = [3, 4];
let result = [...arr1, ...arr2];
console.log(result); // [1, 2, 3, 4]

result = [...[4, 3], ...[2, 1]];
console.log(result); // [4, 3, 2, 1]
```

#### 27.8.8 `Array.prototype.splice`

- push, pop, unshift, shift 메서드 모두 `원본 배열`을 직접 변경하는 메서드이며 `원본 배열`의 처음이나 마지막에 요소를 추가하거나 삭제한다.
- `원본 배열`의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다.
- splice 메서드는 3개의 매개변수가 있으며 `원본 배열`을 직접 변경한다.
  - `start`: `원본 배열`의 요소를 제거하기 시작할 인덱스. start만 지정시 start 부터 모든 요소를 제거한다. start가 음수인 경우 배열의 끝에서의 인덱스를 나타낸다. 만약 start가 -1이면 마지막 요소를 가리키고 -n이면 마지막에서 n번째 요소를가리킨다.
  - `deleteCount`: start부터 제거할 요소의 개수. deleteCount가 0인 경우 아무런 요소도 제거되지 않음(옵션)
  - `items`: 제거한 위치에 삽입할 요소들의 목록. 생략할 경우 `원본 배열`에서 요소들을 제거하기만 함(옵션)

```js
const arr = [1, 1, 5, 6];
const result = arr.splice(1, 1, 2, 3, 4);
console.log(arr); // [ 1, 2, 3, 4, 5, 6 ]
console.log(result); // [1]
```

```js
const arr = [1, 2, 3, 4];
const result = arr.splice(1, 0, 100);
console.log(arr); // [ 1, 100, 2, 3, 4 ]
console.log(result); // []
```

```js
const arr = [1, 2, 3, 4];
const result = arr.splice(1, 2);
console.log(arr); // [ 1, 4 ]
console.log(result); // [2, 3];
```

```js
const arr = [1, 2, 3, 4];
const result = arr.splice(1);
console.log(arr); // [ 1]
console.log(result); // [2, 3, 4]
```

```js
const arr = [1, 2, 3, 4];
const result = arr.splice(1);
console.log(arr);
console.log(result);
```

```js
const arr = [1, 2, 3, 1, 2];

function remove(array, item) {
  const index = array.indexOf(item);

  if (index != -1) {
    array.splice(index, 1);
  }
  return array;
}

console.log(remove(arr, 2)); // [ 1, 3, 1, 2 ]
console.log(remove(arr, 10)); // [ 1, 3, 1, 2 ]
```

#### 27.8.9 `Array.prototype.slice`

- slice 메서드는 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.
- `원본 배열`은 변경하지 않는다
- slice 메서드는 두개의 매개변수를 갖는다
  - `start`: 복사를 시작할 인덱스. 음수인 경우 배열의 끝에서의 인덱스를 나타낸다.
  - `end`: 복사를 종료할 인덱스. 이 인덱스에 해당하는 요소는 복사되지 않는다. `end`는 생략 가능하며 생략 시 기본값은 length 프로퍼티 값이다.

```js
const arr = [1, 2, 3];

arr.slice(0, 1); // [1]

arr.slice(1, 2); // [2]

console.log(arr); // [1, 2, 3]
```

```js
const arr = [1, 2, { a: 3 }];
const copy = arr.slice();

console.log(copy); // [1, 2, { a: 3 }]
console.log(arr === copy); // false
console.log(arr[2] === copy[2]); // true (얕은 복사이므로 같은 객체를 참조)
```

- slice, 스프레드 문법, Object.assign 메서드는 모두 얕은 복사를 수행한다
- 깊은 복사를 위해서는 Lodash 라이브러리의 cloneDeep 메서드를 사용하는 것을 추천한다.

#### 27.8.10 `Array.prototype.join`

- join 메서드는 `원본 배열`의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉, 구분자로 연결한 문자열을 반환한다.
- 구분자는 생략 가능하며 기본 구분자는 콤마(',')다.

```js
const arr = [1, 2, 3, 4];

let result = arr.join();
console.log(result); // 1,2,3,4
console.log(arr); // [ 1, 2, 3, 4 ]

result = arr.join(':');
console.log(result); // 1:2:3:4
console.log(arr); // [ 1, 2, 3, 4 ]
```

#### 27.8.11 `Array.prototype.reverse`

- reverse 메서드는 `원본 배열`의 순서를 반대로 뒤집는다.
- 이때 `원본 배열`이 변경된다. 반환값은 `변경된 배열`이다.

```js
const arr = [1, 2, 3, 4];

let result = arr.reverse();
console.log(result); // [4, 3, 2, 1];
console.log(arr); // [4, 3, 2, 1]
```

#### 27.8.12 `Array.prototype.fill`

- ES6에 도입된 fill 메서드는 인수로 전달받은 값을 `배열`의 처음부터 끝까지 요소로 채운다.
- 이때 `원본 배열`이 변경된다.

```js
const arr = [1, 2, 3, 4];
arr.fill(0);
console.log(arr); // [0, 0, 0, 0]
```

- 두 번째 인수로 요소 채우기를 시작할 인덱스를 전달할 수 있다.

```js
const arr = [1, 2, 3, 4];
arr.fill(0, 2);
console.log(arr); // [ 1, 2, 0, 0 ]
```

- 세 번째 인수로 요소 채우기를 멈출 인덱스를 전달할 수 있다.(인덱스 미포함)

```js
const arr = [1, 2, 3, 4, 5];
arr.fill(0, 1, 3);
console.log(arr); // [1, 0, 0, 4, 5]
```

- `배열`을 생성하면서 특정 값으로 요소 채우기

```js
const arr = new Array(4).fill(4);
console.log(arr); // [4, 4, 4, 4,]
```

- fill 메서드로 요소를 채울 경우 모든 요소를 하나의 값만으로 채울 수 밖에 없는 단점이 있다.
- 하지만, Array.from 메서드를 사용하면 두 번째 인수로 전달한 콜백 함수를 통해 요소값을 만들면서 `배열`을 채울 수 있다.

```js
const sequence = (lenth = 0) => Array.from({ length }, (_, i) => i);
console.log(sequence(3)); // [0, 1, 2]
```

#### 27.8.13 `Array.prototype.includes`

- ES7에 도입된 includes 메서드는 `배열` 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다.
- 첫 번째 인수로 검색할 대상을 지정한다.
- 두 번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
- 두 번째 인수가 생략된 경우 기본값 0으로 설정된다
- 만약 두 번째 인수가 음수를 전달하면 length 프로퍼티 값과 음수 인덱스를 합산하여(length + index) 검색 시작 인덱스를 설정한다.

```js
const fruits = ['apple', 'banana', 'kiwi'];
console.log(fruits.includes('apple')); // true
console.log(fruits.includes('not')); // false

const arr = [1, 2, 3];

console.log(arr.includes(1, 1)); // false
console.log(arr.includes(3, -1)); // true
```

#### 27.8.14 `Array.prototype.flat`

- ES10에서 도입된 flat 메서드는 인수로 전달한 깊이만큼 재귀적으로 `배열`을 평탄화 한다.

```js
[1, [2, 3, 4, 5]].flat(); // [1, 2, 3, 4, 5];

// 중첩 배열을 평탄화하기 위한 깊이 값의 기본값은 1
[1, [2, [3, [4]]]].flat(); // [ 1, 2, [ 3, [ 4 ] ] ]
[1, [2, [3, [4]]]].flat(1); // [ 1, 2, [ 3, [ 4 ] ] ]

[1, [2, [3, [4]]]].flat(2); // [ 1, 2, 3, [ 4 ] ]
[1, [2, [3, [4]]]].flat().flat(); // [ 1, 2, 3, [ 4 ] ]

[1, [2, [3, [4]]]].flat(Infinity); // [ 1, 2, 3, 4 ]
```

## 27.9 배열 고차 함수 <a name= "27.9"></a>

- 고차 함수는 함수를 인수로 전달받거나 반환하는 함수를 말한다
- 함수는 일급 객체이므로 함수를 값처럼 인수로 전달할 수 있으며 반환할 수도 있다.
- 고차 함수는 외부 상태의 변경이나 가변 데이터를 피하고 불변성을 지향하는 함수 프로그래밍에 기반을 두고 있다.
- 함수 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 로직 내에 존재하는 조건문과 반복문을 제거하여 복잡성을 해결하고 변수의 사용을 억제하여 상태 변경을 피하려는 프로그래밍 패러다임이다.
- 함수 프로그래밍은 결국 순수 함수를 통해 부수 효과를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이려는 노력의 일환이라고 할 수 있다.

#### 27.9.1 `Array.prototype.sort`

- sort 메서드는 `배열`의 요소를 정렬한다
- `원본 배열`을 직접 변경하며 `정렬된 배열`을 반환한다.
- default : 오름차순

```js
const fruits = ['Banana', 'Orange', 'Apple', '바나나', '오렌지', '사과'];

// ascending
fruits.sort();
console.log(fruits); // [ 'Apple', 'Banana', 'Orange', '바나나', '사과', '오렌지' ]

// descending
fruits.reverse();
console.log(fruits); // [ '오렌지', '사과', '바나나', 'Orange', 'Banana', 'Apple' ]
```

```js
const points = [40, 100, 1, 5, 2, 25, 10];
points.sort();
console.log(points); // [1, 10, 100, 2, 25, 40, 5]
```

- sort 메서드의 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따른다
- 즉, ``배열``의 요소가 숫자 타입이라 할지라도 ``배열``의 요소를 일시적으로 문자열로 변환한 후 유니코드 코드 포인트의 순서를 기준으로 정렬한다.
- 따라서 숫자 요소를 정렬할 때는 sort 메서드에 **정렬 순서를 정의하는 비교 함수**를 인수로 전달해야 한다.
  - 정렬 함수는 양수나 음수 또는 0을 반환해야 한다
  - 반환 값이 0보다 작으면 비교 함수의 첫 번째 인수를 우선하여 정렬한다
  - 반환 값이 0이면 정렬하지 않는다.
  - 반환 값이 0보다 크면 두 번째 인수를 우선하여 정렬한다.

```js
const points = [40, 100, 1, 5, 2, 25, 10];
// 숫자 배열의 오름차순 정렬
points.sort((a, b) => a - b);
console.log(points); // [1, 2, 5, 10, 25]

// 숫자 배열의 내림차순 정렬
points.sort((a, b) => b - a);

// 객체를 요소로 갖는 배열 정렬
const todos = [
  { id: 4, content: 'JavaScript' },
  { id: 1, content: 'HTML' },
  { id: 2, content: 'CSS' },
];

function compare(key) {
  // 프로퍼티 값이 문자열인 경우 - 산술 연산으로 비교하면 NaN이 나오므로 비교 연산 사용
  // 비교 함수는 양수/음수/0을 반환하면 되므로 - 산술 연산 대신 비교 연산을 사용 가능
  return (a, b) => (a[key] > b[key] ? 1 : a[key] < b[key] ? -1 : 0);
}

todos.sort(compare('id'));
console.log(todos);
/*
[
  { id: 1, content: 'HTML' },
  { id: 2, content: 'CSS' },
  { id: 4, content: 'JavaScript' }
]
*/
todos.sort(compare('content'));
console.log(todos);
/*
[
  { id: 2, content: 'CSS' },
  { id: 1, content: 'HTML' },
  { id: 4, content: 'JavaScript' }
]
*/
```

#### 27.9.2 `Array.prototype.forEach`

- forEach 메서드는 for 문을 대체할 수 있는 고차 함수다.
- `원본 배열`(forEach 메서드를 호출한 배열, 즉 this)을 변경하지 않는다. 하지만 콜백 함수를 통해 `원본 배열`을 변경할 수는 있다.
- forEach의 반환값은 언제나 undefined다.
- forEach 메서드는 break, continue 문을 사용할 수 없다.
- `희소 배열`의 경우 존재하지 않는 요소는 순회 대상에서 제외된다.(map, filter, reduce도 마찬가지)
- 성능은 for문이 더 좋지만 가독성이 forEach가 더좋다
- forEach 메서드는 자신의 내부에서 반복문을 실행한다.
- 즉, froEach 메서드는 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 `호출한 배열`을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.

```js
// for 문 구현
const numbers = [1, 2, 3];
const pows = [];

for (let i = 0; i < numbers.length; ++i) {
  pows.push(numbers[i] ** 2);
}
console.log(pows); // [ 1, 4, 9 ]
```

```js
// forEach 구현
const numbers = [1, 2, 3];
const pows = [];

numbers.forEach((element) => pows.push(element ** 2));
console.log(pows); // [ 1, 4, 9 ]
```

- forEach 메서드의 콜백 함수는 forEach 메서드를 `호출한 배열`의 요소값과 인덱스, forEach 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다.

```js
// forEach 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
[1, 2, 3].forEach((item, index, arr) => {
  console.log(
    `요소값: ${item}, 인덱스 : ${index}, this: ${JSON.stringify(arr)}`
  );
});
/*
요소값: 1, 인덱스 : 0, this: [1,2,3]
요소값: 2, 인덱스 : 1, this: [1,2,3]
요소값: 3, 인덱스 : 2, this: [1,2,3]
*/
```

#### 27.9.3 `Array.prototype.map`

- map 메서드는 자신을 `호출한 배열`의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
- 그리고 콜백 함수의 반환값들로 구성된 `새로운 배열`을 반환한다.
- `원본 배열`은 변경되지 않는다.
- forEach와 같이 자신을 `호출한 배열`의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출 하지만 forEach는 언제나 undefined를 반환하는 반면 map 메서드는 콜백 함수의 반환값들로 구성된 `새로운 배열`을 반환하는 차이가 있다.
- 요소값을 다른 값으로 매핑한 `새로운 배열`을 생성하기 위한 고차 함수다
- map 메서드가 생성하여 반환하는 `새로운 배열`의 length 값은 map 메서드를 `호출한 배열`의 length 프로퍼티 값과 반드시 일치한다.
- map 메서드를 `호출한 배열`의 요소갑소가 인덱스, map 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다

```js
const numbers = [1, 4, 9];

const result = numbers.map((item) => Math.sqrt(item));

console.log(result); // [ 1, 2, 3 ]
console.log(numbers); // [1, 4, 9]
```

#### 27.9.4 `Array.prototype.filter`

- filter 메서드는 자신을 `호출한 배열`의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
- 그리고 콜백 함수의 반환값이 true인 요소로만 구성된 `새로운 배열`을 반환한다.
- 이때 `원본 배열`은 변경되지 않는다.
- filter 메서드는 자신을 호출한 배열에서 필터링 조건을 만족하는 특정 요소만 추출하여 `새로운 배열`을 만들고 싶을 때 사용한다.
- fitler 메서드가 생성하여 반환한 `새로운 배열`의 length 프로퍼티 값은 filter 메서드를 `호출한 배열`의 length 프로퍼티 값과 같거나 작다.
- fitler 메서드를 `호출한 배열`의 요소값, 인덱스, filter 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다.
- filter 메서드를 사용해 특정 요소를 제거할 경우 특정 요소가 중복되어 있다면 중복된 요소가 모두 제거된다. 특정 요소를 하나만 제거하라면 indexOf 메서드를 통해 특정 요소의 인덱스를 취득한 다음 splice 메서드를 사용한다.

```js
const numbers = [1, 2, 3, 4, 5];

const odds = numbers.filter((item) => item % 2);
console.log(odds); // [ 1, 3, 5 ]
```

#### 27.9.5 `Array.prototype.reduce`

- reduce 메서드는 자신을 `호출한 배열`을 모든 요소를 순회하며 전달받은 콜백 함수를 반복 호추한다.
- 그리고 콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 하나의 결과값을 만들어 반환한다.
- 원본 배열은 변경되지 않는다.
- reduce 메서드는 첫 번째 인수로 콜백 함수, 두 번째 인수로 초기값을 전달 받는다
- reduce 메서드의 콜백 함수에는 4개의 인수, 초기값 또는 콜백 함수의 이전 반환값, reduce 메서드를 `호출한 배열`의 요소값과 인덱스, reduce 메서드를 `호출한 배열` 자체, 즉 this가 전달된다.
- reduce 메서드는 자신을 `호출한 배열`의 모든 요소를 순회하며 하나의 결과값을 구해야 하는 경우에 사용한다.
- reduce 메서드를 호출할 때 초기값은 옵션이지만 전달하는 것이 안전하다.

```js
// 2개의 인수, 즉 콜백 함수와 초기값 0을 전달받아 자신을 호출한 배열의 모든 요소를 누적한 결과 반환
const sum = [1, 2, 3, 4].reduce(
  (accumulator, currentValue, index, array) => accumulator + currentValue,
  0
);

console.log(sum); // 10

const sub = [1, 2, 3, 4].reduce(
  (accumulator, currentValue, index, arr) => accumulator - currentValue,
  0
);
console.log(sub); // -10
```

```js
// 평균 구하기
const values = [1, 2, 3, 4, 5, 6];

const average = values.reduce((acc, cur, i, { length }) => {
  // 마지막 순회가 아니면 누적값을 반환하고 마지막 순회면 누적값으로 평균을 구해 반환한다
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(average); // 3.5
```

```js
// 최대값 구하기
const values = [1, 2, 3, 4, 5];

const max = values.reduce((acc, cur) => (acc > cur ? acc : cur), 0);

console.log(max); // 5
```

```js
// 최대값 구하기
// Math.max를 사용하는 방법이 더 직관적
const values = [1, 2, 3, 4, 5];
const max = Math.max(...values);
console.log(max);
```

```js
// 요소의 중복 횟수 구하기
const fruits = ['banana', 'apple', 'orange', 'orange', 'apple'];

const count = fruits.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});

console.log(count); // { banana: 1, apple: 2, orange: 2 }
```

```js
// 중첩 배열 평탄화
// flat 을 사용하는것이 더 직관적
const values = [1, [2, 3], 4, [5, 6]];

// const flatten = values.reduce((acc, cur) => acc.concat(cur), []);
const flatten = values.reduce((acc, cur) => [...acc, ...cur], []);

console.log(flatten); // [ 1, 2, 3, 4, 5, 6 ]
```

```js
// 중복 요소 제거
// reduce, filter(더 직관적), Set(추천)
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];

const result = values.reduce(
  (unique, val, i, _values) =>
    // 현재 순회 중인 요소의 인덱스 i가 val의 인덱스와 같다면 val은 처음 순회하는 요소다
    // 현재 순회 중인 요소의 인덱스 i가 val의 인덱스와 다르다면 val은 중복된 요소다
    // 처음 순회하는 요소만 초기값 []가 전달된 unique 배열에 담아 반환하면 중복된 요소는 제거된다.
    _values.indexOf(val) === i ? [...unique, val] : unique,
  []
);
console.log(result); // [ 1, 2, 3, 5, 4 ]
```

```js
// 중복 요소 제거 filter 사용
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];
// 현재 순회 중인 요소의 인덱스 i가 val의 인덱스와 같다면 val은 처음 순회하는 요소다. 이 요소만 필터링한다.
const result = values.filter((val, i, _values) => _values.indexOf(val) === i);
console.log(result); // [ 1, 2, 3, 5, 4 ]
```

```js
// 중복 요소 제거 Set 사용
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];
const result = [...new Set(values)];
console.log(result); // [ 1, 2, 3, 5, 4 ]
```

#### 27.9.6 `Array.prototype.some`

- some 메서드는 자신을 `호출한 배열`의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.
- 이때 some 메서드는 콜백 함수의 반환값이 단 한 번이라도 참이면 true, 모두 거짓이면 false를 반환한다.
- 즉, `배열`의 요소 중에 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 그 결과를 불리언 타입으로 변환한다.
- 단, some 메서드를 `호출한 배열`이 `빈 배열`인 경우 언제나 false를 반환하므로 주의하기 바란다.
- 메서드를 호출한 요소값과 인덱스, some 메서드를 `호출한 배열` 자체, 즉 this를 순차적을 전달받을 수 있다.

```js
[5, 10, 15].some((item) => item > 10); // true
[5, 10, 15].some((item) => item < 0); // false
['apple', 'banana', 'mango'].some((item) => item === 'banana'); // true

// some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false 반환
[].some((item) => item > 3); // false
```

#### 27.9.7 `Array.prototype.every`

- every 메서드는 자신을 `호출한 배열`의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.
- 이때 every 메서드는 콜백 함수의 반환값이 모두 참이면 true, 단 한 번이라도 거짓이면 false를 반환한다.
- 즉, `배열`의 모든 요소가 콜백 함수를 통해 정의한 조건을 모두 만족하는지 확인하여 그 결과를 불리언 타입으로 반환한다.
- 단 every 메서드를 `호출한 배열`이 `빈 배열`인 경우 언제나 true를 반환하므로 주의하기 바란다.
- 메서드를 호출한 요소값과 인덱스, some 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다.

```js
[5, 10.15].every((item) => item > 3); // true
[5, 10, 15].every((item) => item > 10); // false

// every 메서드를 호출한 배열이 빈 배열인 경우 언제나 true 반환
[].every((item) => item > 3); // true
```

#### 27.9.8 `Array.prototype.find`

- ES6에 도입된 find 메서드는 자신을 `호출한 배열`의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소를 반환한다.
- 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 undefined를 반환한다.
- 메서드를 호출한 요소값과 인덱스, find 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다.
- filter 메서드는 콜백 함수의 호출 결과가 true인 요소만 추출한 새로운 배열을 반환한다. 따라서 filter 메서드의 반환값은 언제나 `배열`이다. 하지만 find 메서드는 콜백 함수의 반환값이 true인 첫 번째 요소를 반환하므로 find의 결과값은 `배열`이 아닌 해당 요소값이다.

```js
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' },
];

const result = users.find((user) => user.id === 2);
console.log(result); // { id: 2, name: 'Kim' }
```

#### 27.9.9 `Array.prototype.findIndex`

- ES6에 도입된 findIndex 메서드는 자신을 `호출한 배열`의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소의 인덱스를 반환한다.
- 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 -1을 반환한다.
- 메서드를 호출한 요소값과 인덱스, findIndex 메서드를 `호출한 배열` 자체, 즉 this를 순차적으로 전달받을 수 있다.

```js
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' },
];

let idx = users.findIndex((user) => user.id === 2);
console.log(idx); // 1

idx = users.findIndex((user) => user.name === 'Park');
console.log(idx); // 3

// 위 처럼 프로퍼티 키와 값으로 요소의 인덱스를 구하는 경우 콜백 함수를 추상화 할 수 있다.
function predicate(key, value) {
  return (item) => item[key] === value;
}
// id가 2인 요소의 인덱스 구하기
idx = users.findIndex(predicate('id', 2));
console.log(idx); // 1
// name이 Park인 요소의 인덱스 구하기
idx = users.findIndex(predicate('name', 'Park'));
console.log(idx); // 3
```

#### 27.9.10 `Array.prototype.flatMap`

- ES10에서 도입된 flatMap 메서드는 map 메서드를 통해 생성된 `새로운 배열`을 평탄화한다.
- 즉, map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.

```js
const arr1 = ['hello', 'world'];
const result1 = arr1.map((x) => x.split('')).flat();
console.log(result1);
/*
[
  'h', 'e', 'l', 'l',
  'o', 'w', 'o', 'r',
  'l', 'd'
]
*/
const arr2 = ['hello', 'world'];
const result2 = arr2.flatMap((x) => x.split(''));
console.log(result1);
/*
[
  'h', 'e', 'l', 'l',
  'o', 'w', 'o', 'r',
  'l', 'd'
]
*/
```

- 단 flatMap 메서드는 flat 메서드처럼 인수를 전달하여 평탄화 깊이를 지정할 수는 없고 1단계만 평탄화한다.
- map 메서드를 통해 생성된 `중첩 배열`의 평탄화 깊이를 지정해야 하면 flatMap 메서드를 사용하지 말고 map 메서드와 flat 메서드를 각각 호출한다

```js
const arr = ['hello', 'world'];

// flatMap은 1단계만 평탄화한다.
const result1 = arr.flatMap((str, index) => [index, [str, str.length]]);
console.log(result1); // [ 0, [ 'hello', 5 ], 1, [ 'world', 5 ] ]

// 평탄화 깊이를 지정해야 하면 flatMap 메서드를 사용하지 말고 map 메서드와 flat 메서드를 각각 호출한다
const result2 = arr.map((str, index) => [index, [str, str.length]]).flat(2);
console.log(result2); // [ 0, 'hello', 5, 1, 'world', 5 ]
```
