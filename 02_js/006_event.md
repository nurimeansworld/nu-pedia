# 이벤트 위임

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="../css/reset.css" />
    <style>
      /* 직접 셀렉트 박스 만들기 */
      h2 {
        margin: 30px;
      }

      .cont-select {
        position: relative;
        width: 200px;
      }

      .btn-select {
        width: 100%;
        padding: 13px 14px;
        color: #000;
        font-size: 12px;
        line-height: 14px;
        text-align: left;
        border: 1px solid #c4c4c4;
        box-sizing: border-box;
        border-radius: 10px;
        cursor: pointer;
        background: url("images/icon-Triangle-down.png") right 13px center
          no-repeat;

        /* 말줄임 추가 */
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
      }

      .btn-select:focus {
        outline: 3px solid #f8e4ff;
      }

      .list-member {
        display: none;
        width: 100%;
        overflow: hidden;
        position: absolute;
        left: 0;
        top: 51px;
        background: #fff;
        border: 1px solid #c4c4c4;
        box-shadow: 4px 4px 14px rgba(0, 0, 0, 0.15);
        border-radius: 10px;
      }

      .btn-select.on {
        background: url("images/icon-Triangle-up.png") right 13px center
          no-repeat;
      }

      .btn-select.on + .list-member {
        display: block;
      }

      .list-member li {
        height: 40px;
        padding: 5px 18px;
      }

      .list-member li button {
        display: block;
        height: 30px;
        width: 100%;
        border: none;
        background-color: #fff;
        border-radius: 8px;
        cursor: pointer;

        /* 말줄임 추가 */
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
      }

      .list-member li button:focus,
      .list-member li button:hover {
        background-color: #f8e4ff;
      }
    </style>
  </head>

  <body>
    <h2>셀렉트 박스 만들기</h2>
    <article class="cont-select">
      <button class="btn-select">나의 최애 프로그래밍 언어</button>
      <ul class="list-member"></ul>
    </article>

    <script>
      const listMember = document.querySelector(".list-member");
      const btnSelect = document.querySelector(".btn-select");
      let listArray = ["Python", "Java", "JavaScript", "C#", "C/C++", "test"];

      listArray.forEach((e) => {
        listMember.innerHTML = `${listMember.innerHTML}<li><button type="button">${e}</button></li>`;
      });

      btnSelect.addEventListener("click", (event) => {
        btnSelect.classList.toggle("on");
      });

      listMember.addEventListener("click", (event) => {
        btnSelect.innerText = event.target.innerText;
        btnSelect.classList.remove("on");
      });

      // 수업시간에 공유 된 다른 분들 코드
      // 1. 이런 식으로 innerHTML보다는 createElement로 추가하는 방식이 권장
      // const fragment = document.createDocumentFragment();

      // ['Python', 'Java', 'JavaScript', 'C#', 'C/C++'].forEach(lang => {
      //   const li = document.createElement('li');
      //   const btn = document.createElement('button');
      //   btn.setAttribute('type', 'button');
      //   btn.appendChild(document.createTextNode(lang));
      //   li.appendChild(btn);
      //   fragment.appendChild(li);
      // });
      // list.appendChild(fragment);

      // // 2. 혜진님 코드 - 접근성 고려
      // // list에서 tab을 누르면 리스트 내에서 돈다.
      // const btn = document.querySelector('.btn-select'); //select
      // const ul = document.querySelector('.list-member'); //ul

      // let arr = ["Python", "Java", "JavaScript", "C#", "C/C++"];
      // for (let i = 0; i < arr.length; i++) {
      //   const li = document.createElement("li");
      //   ul.append(li);
      //   li.innerHTML = `<button type='button'>${arr[i]}</button>`;
      // }

      // const listAll = ul.querySelectorAll('button'); // option list
      // const firstOption = ul.querySelector('button'); //option first button
      // const lastOption = listAll[listAll.length - 1]; //option last button

      // const handlClickSelect = function () {
      //   btn.classList.toggle('on');
      //   ul.classList.toggle('on');
      // }
      // const handlClickOption = function (e) {
      //   btn.innerHTML = e.target.innerText;
      //   btn.classList.remove('on');
      //   ul.classList.remove('on');
      //   window.setTimeout(function () {
      //     btn.focus();
      //   }, 100);
      // }

      // //focus 이동
      // const handleTabFoucus = function (e) {
      //   if (!e.shiftKey && e.keyCode === 9) {
      //     e.preventDefault();
      //     window.setTimeout(function () {
      //       firstOption.focus();
      //     }, 100);
      //   }
      // };
      // //shift+tab
      // const handlShiftTabFoucus = function (e) {
      //   if (e.shiftKey && e.keyCode === 9) {
      //     e.preventDefault();
      //     window.setTimeout(function () {
      //       lastOption.focus();
      //     }, 100);
      //   }
      // };
      // //ESC키
      // const hadleEsc = function (e) {
      //   if (e.keyCode === 27) {
      //     btn.classList.remove('on');
      //     ul.classList.remove('on');
      //     window.setTimeout(function () {
      //       btn.focus();
      //     }, 100);
      //   }
      // }

      // btn.addEventListener('click', handlClickSelect);
      // ul.addEventListener('click', handlClickOption);

      // btn.addEventListener('keydown', hadleEsc);
      // ul.addEventListener('keydown', hadleEsc);

      // lastOption.addEventListener('keydown', handleTabFoucus);
      // firstOption.addEventListener('keydown', handlShiftTabFoucus);

      // // 3. 수철님 코드
      // // 이런 식으로 $에 함수를 넣어서 표시하는 방식도 가능하지만 jQuery랑 헷갈릴 수 있으니 개념만 잘 알아두자..!
      // const $ = (selector) => document.querySelector(selector);
      // $('.btn-select').addEventListener("click", function (event) {
      //   event.target.classList.toggle("on");
      // })

      // // 4.
      // // 이벤트 위임의 경우 안전하게 if문으로 타겟 범위를 잘 설정해주어야 한다.
      // // 안그럼 다 선택되어서 PythonJavaJavaScript... 이런식으로 값 설정이 되기도ㅠㅠ
      // list.addEventListener('click', (event) => {
      //   if (event.target.nodeName === "BUTTON") {
      //     btn.innerText = event.target.innerText;
      //     btn.classList.remove('on');
      //   }
      // });
    </script>
  </body>
</html>
```
