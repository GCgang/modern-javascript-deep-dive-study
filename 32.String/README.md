# 32장 String

표준 빌트인 객체인 String은 원시 타입인 문자열을 다룰 때 유용한 프로퍼티와 메서드를 제공한다.

## 목차

- [String 생성자 함수](#32.1)
- [String length 프로퍼티](#32.2)
- [String 메서드](#32.3)

## 32.1 String 생성자 함수 <a name= "32.1"></a>

- 표준 빌트인 객체인 String 객체는 생성자 함수 객체다. 따라서 new 연산자와 함께 호출하여 String 인스턴스를 생성할 수 있다.
- 배열과 유사하게 인덱스를 사용하여 각 문자에 접근할 수 있다.
- 생성자 함수에 인수로 문자열이 아닌 값을 전달하면 인수를 문자열로 강제 변환한 후, 변환된 문자열을 할당한 객체를 생성한다.
- new 연산자를 사용하지 않고 String 생성자 함수를 호출하면 String 인스턴스가 아닌 문자열을 반환한다. 이를 이용하여 명시적으로 타입을 변환하기도 한다.

  ```js
  const strObj = new String();
  console.log(strObj); // String {''}

  const strObj2 = new String('An');
  console.log(strObj2); // String {'An'}

  console.log(strObj2[0]); // 'A'

  const strObj3 = new String(null);
  console.log(strObj3); // String {'null'}

  const strObj4 = new String(123);
  console.log(strObj4); // String {'123'}

  console.log(String(123)); // 123
  console.log(String(null)); // null
  console.log(String(NaN)); // NaN
  console.log(String(Infinity)); // Infinity
  console.log(String(true)); // true
  console.log(String(false)); // false
  ```

## 32.2 String length 프로퍼티 <a name= "32.2"></a>

- length 프로퍼티는 문자열의 문자 개수를 반환한다.
  ```js
  console.log('Hello'.length); // 5
  console.log('안녕하세요'.length); // 5
  ```

## 32.3 String 메서드 <a name= "32.3"></a>

- 배열의 경우 원본 배열을 직접 변경하는 메서드와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드가 있다.
- 하지만 String 객체에는 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다.
- 즉, String 객체의 메서드는 언제나 새로운 문자열을 반환한다.
- 문자열은 변경 불가능한 원시 값이기 때문에 String 래퍼 객체도 읽기 전용 객체로 제공된다.

### 32.3.1 String.prototype.indexOf

- indexOf 메서드는 대상 문자열(메서드를 호출한 문자열)에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환한다.
- 검색에 실패하면 -1을 반환한다
- 역순으로 탐색하는 lastIndexOf()도 있다.

  ```js
  const str = 'Hello World';

  str.indexOf(l); // 2

  str.indexOf('or'); // 7

  str.indexOf('x'); // -1
  ```

- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
  ```js
  str.indexOf('l', 3); // 3
  ```
- 대상 문자열에 특정 문자열이 존재하는지 확인할 때 유용하다.
  ```js
  if (str.indexOf('Hello') !== -1) {
    console.log('Hello 찾음'); // Hello 찾음
  }
  ```

### 32.3.1 String.prototype.search

- search 메서드는 대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다.
- 검색에 실패하면 -1을 반환한다.

  ```js
  const str = 'Hello, world';

  str.search(/o/); // 4
  str.search(/x/); // -1
  ```

### 32.3.1 String.prototype.includes

- ES6에 도입된 includes 메서드는 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 그 결과를 true 또는 false로 반환한다.

  ```js
  const str = 'Hello, World';

  str.includes('Hello'); // true
  str.includes(','); // true
  str.includes(' '); // true
  str.includes(' W'); // true
  str.includes('x'); // false
  ```

- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
  ```js
  str.includes(',', 5); // true
  str.includes(',', 6); // false
  ```

### 32.3.1 String.prototype.startsWith

- ES6에 도입된 startsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 그 결과를 true 또는 false로 반환한다.

  ```js
  const str = 'Hello, World';

  str.startsWith('H'); // true
  str.startsWith('He'); // true
  str.startsWith('x'); // false
  ```

- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
  ```js
  str.startsWith(' '); // false
  str.startsWith(' ', 6); // true
  ```

### 32.3.1 String.prototype.endsWith

- ES6에 도입된 endsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 true 또는 false로 반환한다.

  ```js
  const str = 'Hello, World';

  str.endsWith('d'); // true
  str.endsWith('ld'); // true
  str.endsWith(''); // true
  str.endsWith('He'); // false
  ```

- 2번째 인수로 검색할 문자열의 길이를 전달할 수 있다.

  ```js
  str.endsWith(' '); // false
  str.endsWith(' ', 7); // true
  ```

### 32.3.1 String.prototype.charAt

- charAt 메서드는 대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.
- 인덱스는 문자열의 범위 (0 ~ 문자열 -1) 사이의 정수이어야 한다.
- 인덱스가 문자열의 범위를 벗어난 정수인 경우 빈 문자열을 반환한다.
- 유사한 문자열 메서드로 charCodeAt, codePointAt이 있다.

  ```js
  const str = 'Hello';

  for (let i = 0; i < str.length; ++i) {
    console.log(str.charAt(i)); // H e l l o
  }

  console.log(str.charAt(10)); // ''
  ```

### 32.3.1 String.prototype.substring

- substring 메서드는 대상 문자열에서 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.
- 두 번째 인수는 생략할 수 있다. 이때 첫 번째 인수로 전달한 인덱스에 위치하는 문자부터 마지막 문자까지 부분 문자열을 반환한다.

  ```js
  const str = 'Hello, World';

  str.substring(0, 5); // Hello
  str.substring(5, 6); // ,
  str.substring(7); // World
  str.substring(-2); // Hello, World
  str.substring(100); // ''
  ```

- indexOf 와 함께 사용하여 특정 문자열을 기준으로 앞뒤에 위치한 부분 문자열 취득하기
  ```js
  str.substring(0, str.indexOf(',')); // Hello
  str.substring(str.indexOf(' ') + 1, str.length); // World
  ```

### 32.3.1 String.prototype.slice

- slice 메서드는 substring 메서드와 동일하게 동작한다.
- 단, slice 메서드에는 음수인 인수를 전달할 수 있다.
- 음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

  ```js
  const str = 'Hello, World';

  str.slice(0, 5); // Hello
  str.slice(5, 6); // ,
  str.slice(7); // World
  str.slice(-2); // ld
  str.slice(-5); // World
  ```

### 32.3.1 String.prototype.toUpperCase

- toUpperCase 메서드는 대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.
  ```js
  const str = 'Hello, World';
  str.toUpperCase(); // 'HELLO, WORLD'
  ```

### 32.3.1 String.prototype.toLowerCase

- toLowerCase 메서드는 대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.
  ```js
  const str = 'Hello, World';
  str.toLowerCase(); //'hello, world'
  ```

### 32.3.1 String.prototype.trim

- trim 메서드는 대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.
  ```js
  const str = '    foo    ';
  str.trim(); // foo
  str.trimStart(); // 'foo    '
  str.trimEnd(); // '    foo'
  ```

### 32.3.1 String.prototype.repeat

- ES6에 도입된 repeat 메서든느 대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환한다.
- 인수로 전달받은 정수가 0이면 빈 문자열을 반환한다
- 인수로 전달받은 정수가 음수이면 RangeError를 발생시킨다.
- 인수를 생략하면 기본값 0이 설정된다

  ```js
  const str = 'abc';

  str.repeat(); // ''
  str.repeat(0); // ''
  str.repeat(1); // 'abc'
  str.repeat(-1); // Uncaught RangeError
  str.repeat(2); // 'abcabc'
  str.repeat(3.5); // 'abcabcabc'
  ```

### 32.3.1 String.prototype.replace

- replace 메서드는 대상문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환한다.
- 검색된 문자열이 여럿 존재할 경우 첫 번째로 검색된 문자열만 치환한다.
- 두번째 인수로 치환 함수를 전달할 수 있다.

  ```js
  const str = 'Hello World World';

  str.replace('World', 'An'); // 'Hello An World'
  str.replace('Wo', 'An'); // 'Hello Anrld World'
  ```

### 32.3.1 String.prototype.split

- split 메서드는 대상 문자열에서 첫 번째 인수로 전달한 문자열 또는 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.
- 인수로 빈 문자열을 전달하면 각 문자를 모두 분리한다.
- 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.

  ```js
  const str = 'How are you doing?';
  str.split(); // ['How are you doing?']
  str.split(''); // ['H', 'o', 'w', ' ', 'a', 'r', 'e', ' ', 'y', 'o', 'u', ' ', 'd', 'o', 'i', 'n', 'g', '?']
  str.split(' '); // ['How', 'are', 'you', 'doing?']
  str.split(/\s/); // ['How', 'are', 'you', 'doing?']
  str.split('How'); // ['', ' are you doing?']
  ```

- 두 번째 인수로 배열의 길이를 지정할 수 있다.
  ```js
  str.split(' ', 2); // ['How', 'are']
  ```
- split, reverse, join 사용하여 문자열 역순으로 뒤집기
  ```js
  str.split('').reverse().join(''); // '?gniod uoy era woH'
  ```
