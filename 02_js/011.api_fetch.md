# api 연동하기
## fetch()
[공식 문서](https://developer.mozilla.org/en-US/docs/Web/API/fetch)
```js
// 순서대로
function 함수이름() {
  const res = fetch({resource}, {init-optional});
}
```
1. await 선언 필요 : 로그인 동작은 비동기로 이뤄져야 하기 때문에, async & await을 사용했고, 이 2개는 반드시 동시에 사용되어야 올바른 데이터 처리 가능
2. res에 있는 fetch 값 : 기본적으로 api 문서에 명세되어있는 내용을 보고 채우면 됨. method, headers, body 크게 3가지로 보통 명시되어 있음.
3. body 값 형변환 : jSON.stringify를 하지 않으면 object 형태로 return 되기 때문에 우리가 처리하려는 string 형변환 해야 함.
4. try{}catch(){} : 동작 수행 후 예외처리를 위해 선언. catch(err)로 err 내용 확인 가능. 정확한 원리는 추후 확인 필요.

```js
// 예제 코드
async function login(e) {
  e.preventDefault(); // button form 전송하지 않게 초기화

  const userEmail = loginEmailInput.value;
  const userPw = loginPwInput.value;
  const url = "http://******";
  const loginData = {
    "user": {
      "email": userEmail,
      "password": userPw
    }
  };

  try{
    const res = await fetch(url+'/user/login', {
      method: "POST",
      headers: {
        "Content-type" : "application/json"
      },
      body: JSON.stringify(loginData),
    });
    const resJson = await res.json();
    console.log('resJson', resJson);

    if(resJson.status == 200){ // 로그인 성공한 경우
      localStorage.setItem("Token",resJson.user.token);
      location.href = "./H01.html";
    }else{ // 로그인 실패한 경우
      LoginError.style.display = 'block'; // LoginError.classList.add = 'on';
      LoginError.textContent = resJson.message;
    }
  }catch(err){
    // 아예 api와 연결이 되지 않았을 때
    // console.log('err', err);
  } 
}
largeNextBtn.addEventListener('click', login);
```