# 정규식(후에 추가하자)

1. 정규식 체크 방법
```js
const regExp = new RegExp('^[가-힣]+$');
console.log(regExp.test(e.target.value));

const regExp = '/^[가-힣]+$/';
console.log(e.target.value.match(e.target.value));
```
test 는 true, false 반환이고 사용하려면 new RegExp('{/가 안들어간다 완전 중요.}');
match 는 일치하는 값을 반환이고 사용하려면 그냥 string으로. 대신 /가 앞뒤로 들어간다.