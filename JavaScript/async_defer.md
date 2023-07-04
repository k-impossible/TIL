## head에서 참조
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
	<script src="main.js"></script>
</head>
<body></body>
</html>
```
#### 브라우저 로드 순서
1. html 다운로드
2. js 다운로드 **----[ blocking ]**
3. js 실행 **----[ blocking ]**
4. html 다운로드
5. 페이지 렌더링 완료

js를 참조하는 가장 기본적인 방법이지만 가장 안좋은 방법이다. js파일 사이즈가 클 경우 화면 로딩이 길어지고 js 실행 단계에서 html요소를 모두 읽어온 상태가 아니어서 js에서 html요소를 조작하는 구문이 있을 시 에러가 발생한다.

## body 끝에서 참조
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    ...
    ...
    ...
	<script src="main.js"></script>
</body>
</html>
```
#### 브라우저 로드 순서
1. html 다운로드
2. 페이지 렌더링 완료
3. js 다운로드 **----[ loading ]**
4. js 실행

html을 모두 다운받은 뒤에 js를 다운받아오기 때문에 페이지 렌더링은 빠르지만 js를 이용해서 데이터를 받아오거나 스타일,애니메이션 등의 처리 작업이 있다면 유저에게 정상적인 페이지를 보여주기 위해 시간이 다소 필요하다.

## async 속성
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
	<script async src="main.js"></script>
</head>
<body></body>
</html>
```
#### 브라우저 로드 순서
1. html, js 다운로드
2. js 실행 **----[ blocking ]**
3. html 다운로드
4. 페이지 렌더링 완료

html을 다운받는 동시에 js를 다운받기 때문에 js다운로드 시간을 절약할 순 있지만 js실행 단계에서 여전히 페이지 로딩이 지체되고 html요소 조작시 에러가 발생할 수 있다. 여러개의 js를 참조할때 참조 순서 대로 실행되어야 한다면 async옵션은 다운로드가 먼저 완료된 js부터 실행하기 때문에 문제가 발생한다.

## defer 속성
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
	<script defer src="main.js"></script>
</head>
<body></body>
</html>
```
#### 브라우저 로드 순서
1. html, js 다운로드
2. 페이지 렌더링 완료
3. js 실행

html을 다운받는 동시에 js를 다운받고 페이지 렌더링이 완료된 후에 js를 실행하기 때문에 페이지 로딩도 빠르고 html요소 조작도 문제없이 실행된다. 여러개의 js를 참조할때도 참조 순서대로 실행되기 때문에 가장 안전한 참조 방법이다.

<br>

> [javascript.info - defer,async 스크립트](https://ko.javascript.info/script-async-defer)
