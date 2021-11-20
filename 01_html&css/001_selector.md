# 1. 선택자(부모와 자식, 조상과 자손)

## 정리

```html
<!DOCTYPE html>

<body>
  <section>
    <h1>헷갈리는 선택자~</h1>
    <article class="first">
      <p>부모 자식 선택자</p>
    </article>
    <article class="second">
      <p>조상 자손 선택자</p>
    </article>
  </section>
</body>

</html>
```

### 부모와 자식

- 부모 : 해당 요소의 바로 상위 요소. only one
- 자식 : 해당 요소의 바로 하위 요소. not only one
- 위의 코드의 경우
  - section 태그의 부모 요소는 body 태그
  - section 태그의 자식 요소는 h1, article, article 태그

### 조상과 자손

- 조상 : 해당 요소의 모든 상위 요소
- 자손 : 해당 요소의 모든 하위 요소
- 위의 코드의 경우
  - section 태그의 조상 요소는 body 태그
  - section 태그의 자손 요소는 h1, article, p, article, p 태그
  - article class="first"의 조상 요소는 section, body 태그
  - article class="first"의 자손 요소는 p 태그

## 헷갈렸던 부분

부모와 자식까지는 잘 알았어도 조상과 자손이 헷갈려서 다시 정리해보았당ㅎㅎ
