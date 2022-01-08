# 시간을 필요한 정보로 각각 받아오기
[공식 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date)
- `.getFullYear()` : return 현지시간 기준 연도 4자리
- `.getMonth()` : return .. 월(0~11)
- `.getDate()` : return  일(1~31)
- `.getDay()` : return .. 요일(0~6)
- `.getHours()` : return .. 시(0~23)
- `.getMinutes()` : return .. 분(0~59)
- `.getSecond()` : return .. 초(0~59)
- `.getTime()` : return 1970-01-01 00:00:00 기준 밀리초 단위

```js
let today = new Date();

// 아래와 같이 직접 지정도 가능
let birthday = new Date('December 17, 1995 03:24:00');
let birthday = new Date('1995-12-17T03:24:00');
let birthday = new Date(1995, 11, 17);            // 월은 0부터 시작
let birthday = new Date(95, 11, 17, 3, 24, 0);

console.log(today);
console.log(birthday);

console.log(today.getFullYear());
console.log(today.getMonth());
console.log(today.getDate());
console.log(today.getDay());

console.log(today.getHours());
console.log(today.getMinutes());
console.log(today.getSeconds());
```