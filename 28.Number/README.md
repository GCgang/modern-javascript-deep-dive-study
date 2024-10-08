# 28장 Number

표준 빌트인 객체인 Number는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다.

## 목차

- [Number 생성자 함수](#28.1)
- [Number 프로퍼티](#28.2)
- [Number 메서드](#28.3)

## 28.1 Number 생성자 함수 <a name= "28.1"></a>

- 표준 빌트인 객체인 Number 객체는 생성자 함수 객체다.

  ```js
  const numObj = new Number();
  console.log(numObj); // Number {0}
  ```

- Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 인수를 강제 변환한 후, 변환된 숫자를 할당한 객체를 생성한다.

  ```js
  let numObj = new Number('10');
  console.log(numObj); // Number {10}

  numObj = new Number('Hello');
  console.log(numObj); // Number {NaN}
  ```

- new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 숫자가 반환되는 것을 활용하여 명시적으로 타입을 변환하기도 한다.
  ```js
  Number('0'); // 0
  Number('-1'); // -1
  Number('10.53'); // 10.53
  Number(true); // 1
  Number(false); // 0
  ```

## 28.2 Number 프로퍼티 <a name= "28.2"></a>

### 28.2.1 Number.EPSILON

- 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다.
- 약 2.2204460492503130808472633361816 x 10<sup>-16</sup> 이다.(이것은 0.000000000000000222 정도로 매우 작은 숫자라는 뜻)
- 아래 예제와 같이 부동소수점 산술 연산은 정확한 결과를 기대하기 어렵다. 정수는 2진법으로 오차 없이 저장 가능하지만 부동소수점을 표현하기 위해 널리 쓰이는 표준인 IEEE 754는 2진법으로 변환했을 때 무한소수가 되어 미세한 오차가 발생할 수밖에 없는 구조적 한계가 있다.
  ```js
  0.1 + 0.2; // 0.30000000000000004
  0.1 + 0.2 === 0.3; // false
  ```
- Number.EPSILON은 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다

  ```js
  function isEqual(a, b) {
    // a와 b를 뺀 값의 절대값이 Number.EPSILON보다 작으면 같은 수로 인정한다.
    return Math.abs(a - b) < Number.EPSILON;
  }

  isEqual(0.1 + 0.2, 0.3); // true
  ```

### 28.2.2 Number.MAX_VALUE

- 자바스크립트에서 표현할 수 있는 가장 큰 양수 값(1.7976931348623157 × 10<sup>308</sup>)이다.
- Number.MAX_VALUE보다 큰 숫자는 Infinity다.
  ```js
  Number.MAX_VALUE; // 1.7976931348623157e+308
  Infinity > Number.MAX_VALUE; // true
  ```

### 28.2.3 Number.MIN_VALUE

- 자바스크립트에서 표현할 수 있는 가장 작은 양수 값(5 x 10<sup>-324</sup>)이다.
- Number.MIN_VALUE보다 작은 숫자는 0이다.
  ```js
  Number.MIN_VALUE; // 5e-324
  Number.MIN_VALUE > 0; // true
  ```

### 28.2.4 Number.MAX_SAFE_INTEGER

- 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값(9007199254740991)이다(이 숫자까지는 모든 정수를 정확하게 표현할 수 있다는 뜻)
  ```js
  Number.MAX_SAFE_INTEGER; // 9007199254740991
  ```

### 28.2.5 Number.MIN_SAFE_INTEGER

- 자바스크립트에서 안전하게 표현할수 있는 가장 작은 정수값(-9007199254740991)이다.(이 숫자까지는 모든 정수를 정확하게 표현할 수 있다는 뜻)
  ```js
  Number.MIN_SAFE_INTEGER; // -9007199254740991
  ```

### 28.2.6 Number.POSITIVE_INFINITY

- 양의 무한대를 나타내는 숫자값 Infinity와 같다
  ```js
  Number.POSITIVE_INFINITY; // Infinity
  ```

### 28.2.7 Number.NEGATIVE_INFINITY

- 음의 무한대를 나타내는 숫자값 -Infinity와 같다
  ```js
  Number.NEGATIVE_INFINITY; // -Infinity
  ```

### 28.2.8 Number.NaN

- 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다. Number.Nan은 window.NaN과 같다.
  ```js
  Number.NaN; // NaN
  ```

## 28.3 Number 메서드 <a name= "28.3"></a>

### 28.3.1 Number.isFinite

- 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity 또는 -Infinity가 아닌지 검사하여 그 결과를 불리언 값으로 반환한다.

  ```js
  // 인수가 정상적인 유한수이면 true를 반환한다.
  Number.isFinite(0); // true
  Number.isFinite(Number.MAX_VALUE); // true
  Number.isFinite(Number.MIN_VALUE); // true

  // 인수가 무한수이면 false를 반환한다.
  Number.isFinite(Infinity); // false
  Number.isFinite(-Infinity); // false

  // 인수가 NaN이면 언제나 false를 반환한다.
  Number.isFinite(NaN); // false

  // Number.isFinite는 인수를 숫자로 암묵적 타입 변환하지 않는다.
  Number.isFinite('1'); // false
  Number.isFinite(null); // false

  // 빌트인 전역 함수 isFinite는 전달받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행한다.
  isFinite('1'); // true
  isFinite(null); // true
  ```

### 28.3.2 Number.isInteger

- 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환한다. 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

  ```js
  Number.isInteger(0); // true
  Number.isInteger(123); // true
  Number.isInteger(-123); // true

  Number.isInteger(0.5); // false
  Number.isInteger('123'); // false
  Number.isInteger(false); // false
  Number.isInteger(Infinity); // false
  Number.isInteger(-Infinity); // false
  ```

### 28.3.3 Number.isNaN

- 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 변환한다.

  ```js
  // 인수가 NaN이면 true를 반환한다.
  Number.isNaN(NaN); // true

  // Number.isNaN은 인수를 숫자로 암묵적 타입 변환하지 않는다.
  Number.isNaN(undefined); // false
  Number.isNaN('a' + 1); // false

  // isNaN은 인수를 숫자로 암묵적 타입 변환한다. undefined는 NaN으로 암묵적 타입 변환된다.
  isNaN(undefined); // true
  isNaN('a' + 1); // true
  ```

### 28.3.4 Number.isSafeInteger

- 인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.
- 안전한 정수값은 -(2<sup>53</sup> - 1)과 2<sup>53</sup> - 1 사이의 정수값이다.
- 검사전에 인수를 숫자로 암묵적 타입 변환하지 않는다.
  ```js
  Number.isSafeInteger(0); // true
  Number.isSafeInteger(1000000000000000); // true
  Number.isSafeInteger(10000000000000001); // false
  Number.isSafeInteger(0.5); // false
  Number.isSafeInteger('123'); // false
  Number.isSafeInteger(false); // false
  Number.isSafeInteger(Infinity); // false
  ```

### 28.3.5 Number.prototype.toExponential

- 숫자를 지수 표기법으로 변환하여 문자열로 변환한다.
- 지수 표기법 : 매우 크거나 작은 숫자를 표기할 때 주로 사용하며 e(Exponent) 앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 나타내는 방식이다. 인수로 소수점 이하로 표현할 자릿수를 전달할 수 있다.
  ```js
  (77.1234).toExponential(); // '7.71234e+1'
  (77.1234).toExponential(4); // '7.7123e+1'
  (77.1234).toExponential(2); // '7.71e+1'
  ```

### 28.3.6 Number.prototype.toFixed

- 숫자를 반올림하여 문자열로 반환한다.
- 반올림하는 소수점 이하 자릿수를 나타내는 0 ~ 20 사이의 정수값을 인수로 전달할 수 있다. 인수를 생략하면 기본값이 0이 지정된다.
  ```js
  (12345.6789).toFixed(); // '123456'
  (12345.6789).toFixed(1); // '12345.7'
  (12345.6789).toFixed(2); // '12345.68'
  (12345.6789).toFixed(3); // '12345.679'
  ```

### 28.3.7 Number.prototype.toPrecision

- 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.
- 인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.
- 전체 자릿수를 나타내는 0 ~ 21 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 0이 지정된다.

  ```js
  (12345.6789).toPrecision(); // '12345.679'
  (12345.6789).toPrecision(5); // '12346'
  (12345.6789).toPrecision(6); // '12345.7'

  (12345.6789).toPrecision(1); // '1e+4'
  (12345.6789).toPrecision(2); // '1.2e+4'
  ```

### 28.3.8 Number.prototype.toString

- 숫자를 문자열로 변환하여 반환한다.
- 진법을 나타내는 2 ~ 36 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 10진법이 지정된다.
  ```js
  (10).toString(); // '10'
  (16).toString(2); // '10000'
  (16).toString(8); // '20'
  (16).toString(16); // '10'
  ```
