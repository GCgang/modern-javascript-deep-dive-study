# 44장 REST API

REST는 HTTP 프로토콜을 의도에 맞게 디자인하도록 유도하고 있다. REST의 기본 원칙을 성실히 지킨 서비스 디자인을 RESTful이라고 표현한다
즉, REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처고, REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미한다.

## 목차

- [REST API의 구성](#44.1)
- [REST API 설계 원칙](#44.2)
- [JSON Server를 이용한 REST API 실습](#44.3)

## 44.1 REST API의 구성 <a name= "44.1"></a>

- REST API는 자원, 행위, 표현의 3가지 요소로 구성된다
- REST는 자체 표현 구조로 구성되어 REST API만으로 HTTP 요청의 내용을 이해할 수 있다.
  | 구성 요소 | 내용 | 표현 방법 |
  | -------- | --- | ------- |
  | 자원 `resource` | 자원 | URI(엔드포인트) |
  | 행위 `verb` | 자원에 대한 행위 | HTTP 요청 메서드 |
  | 표현 `representations` | 자원에 대한 행위의 구체적 내용 | 페이로드 |

## 44.2 REST API 설계 원칙 <a name= "44.2"></a>

REST에서 가장 중요한 기본원칙 두가지

- URI는 리소스를 표현해야 한다

  - 리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용한다. 따라서 이름에 get 같은 행위에 대한 표현이 들어가서는 안 된다.

  ```js
  # bad
  GET /getOdos/1
  GET /tods/show/1

  # good
  GET /todos/1
  ```

- 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.

  - HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적(리소스에 대한 행위)을 알리는 방법이다
  - 주로 5가지 요청 메서드(GET, POST, PUT, PATCH, DELETE 등)를 사용하여 CRUD를 구현한다.
    <img src='./요청 메서드.png' alt='요청 메서드'/>
  - 리소스에 대한 행위는 HTTP 요청 메서드를 통해 표현하며 URI에 표현하지 않는다. 예를 들어 리소스를 취득하는 경우에는 GET, 리소스를 삭제하는 경우에는 DELETE를 사용하여 리소스에 대한 행위를 명확히 표현한다.

  ```js
  # bad
  GET /todos/delete/1

  # good
  DELETE /todos/1
  ```

## 44.3 Server를 이용한 REST API 실습 <a name= "44.3"></a>

- JSON Server를 사용해 REST API 서버를 구축하여 HTTP 요청을 전송하고 응답을 받는 실습 진행

### 44.3.1 JSON Server 설치

- JSON Server는 json 파일을 사용하여 가상 REST API 서버를 구축할 수 있는 툴이다

```bash
npm init -y

npm install json-server --save-dev
```

### 44.3.2 db.json 파일 생성

- 프로젝트 루트 폴더에 db.json 파일 생성
- db.json 파일은 리소스를 제공하는 데이터 베이스 역할

  ```json
  {
    "todos": [
      {
        "id": 1,
        "content": "HTML",
        "completed": true
      },
      {
        "id": 2,
        "content": "CSS",
        "completed": false
      },
      {
        "id": 3,
        "content": "JavaScript",
        "completed": true
      }
    ]
  }
  ```

### 44.3.3 JSON Server 실행

- JSON Server 실행
- JSON Server가 데이터베이스 역할을 하는 db.json 파일의 변경을 감지하게 하려면 watch 옵션을 추가한다.

  ```bash
  ## 기본 포트 (3000) 사용 / watch 옵션 적용
  json-server --watch db.json
  ```

  기본 포트는 3000이다. 포트를 변경하려면 port 옵션을 추가한다.

  ```bash
  ## 포트 변경 / watch 옵션 적용
    json-server --watch db.json --port 5000

  ```

### 44.3.4 GET 요청

- todos 리소스에서 모든 todo를 취득(index)한다.
- JSON Server의 루트 폴더에 public 폴더 생성 후 get_index.html을 추가한다.
- http://localhost:3000/get_index.html 로 접속한다

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('GET', '/todos');
      xhr.send();
      xhr.onload = () => {
        if (xhr.status === 200) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// todos 취득
[
  {
    "id": "1",
    "content": "HTML",
    "completed": true
  },
  {
    "id": "2",
    "content": "CSS",
    "completed": false
  },
  {
    "id": "3",
    "content": "JavaScript",
    "completed": true
  }
]
```

- todos 리소스에서 id를 사용하여 특정 todo를 취득하기
- public 폴더에 get_retrieve.html을 추가한다.
- http://localhost:3000/get_retrieve.html 로 접속한다

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('GET', '/todos/1');
      xhr.send();
      xhr.onload = () => {
        if (xhr.status === 200) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// 특정 todo 취득
{
  "id": "1",
  "content": "HTML",
  "completed": true
}
```

### 44.3.5 POST 요청

- todos 리소스에 새로운 todo를 생성한다
- POST 요청 시에는 setRequestHeader 메서드를 사용하여 요청 몸체에 담아 서버로 전송할 페이로드의 MIME 타입을 지정해야 한다
- public 폴더에 post.html을 추가한다
- http://localhost:3000/post.html 로 접속한다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('POST', '/todos');
      xhr.setRequestHeader('content-type', 'application/json');
      xhr.send(JSON.stringify({ id: 4, content: 'React', completed: false }));
      xhr.onload = () => {
        if (xhr.status === 200 || xhr.status === 201) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// 추가된 todo
{
  "id": 4,
  "content": "Angular",
  "completed": false
}
```

### 44.3.6 PUT 요청

- PUT은 특정 리소스 전체를 교체할 때 사용한다.
- todos 리소스에서 id로 todo를 특정하여 id를 제외한 리소스 전체를 교체한다
- PUT 요청 시에는 setRequestHeader 메서드를 사용하여 요청 몸체에 담아 서버로 전송할 페이로드의 MIME 타입을 지정해야 한다.
- public 폴더에 put.html을 추가한다
- http://localhost:3000/put.html 로 접속한다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('PUT', '/todos/4');
      xhr.setRequestHeader('content-type', 'application/json');
      xhr.send(JSON.stringify({ id: 4, content: 'React', completed: true }));
      xhr.onload = () => {
        if (xhr.status === 200) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// 변경된 todo
{
  "id": "4",
  "content": "React",
  "completed": true
}
```

### 44.3.7 PATCH 요청

- PATCH는 특정 리소스의 일부를 수정할 때 사용한다.
- todo 리소스의 id로 todo를 특정하여 completed만 수정한다
- PATCH 요청 시에는 setRequestHeader 메서드를 사용하여 요청 몸체에 담아 서버로 전송할 페이로드의 MIME 타입을 지정해야 한다.
- public 폴더에 patch.html을 추가한다.
- http://localhost:3000/patch.html 로 접속한다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('PATCH', '/todos/4');
      xhr.setRequestHeader('content-type', 'application/json');
      xhr.send(JSON.stringify({ completed: false }));
      xhr.onload = () => {
        if (xhr.status === 200) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// 일부 수정된 todo
{
  "id": "4",
  "content": "React",
  "completed": false
}
```

### 44.3.8 DELETE 요청

- todo 리소스에서 id를 사용하여 todo를 삭제한다.
- public 폴더에 delete.html을 추가한다.
- http://localhost:3000/delete.html 로 접속한다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <pre></pre>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open('DELETE', '/todos/4');
      xhr.send();
      xhr.onload = () => {
        if (xhr.status === 200) {
          document.querySelector('pre').textContent = xhr.response;
        } else {
          console.error('Error', xhr.status, xhr.statusText);
        }
      };
    </script>
  </body>
</html>
```

```json
// 삭제된 todo
{
  "id": "4",
  "content": "React",
  "completed": false
}
```
