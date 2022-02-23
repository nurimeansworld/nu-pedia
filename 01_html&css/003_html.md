### section vs article

- article은 독립적, section은 연관적
- 똑 떼어서 사용 가능한 부분이면 article 그 외의 부분이면 section이라고 생각하는게 좋을 듯 하다

### radio vs checkbox

- radio는 중복 선택 불가
  - radio name=“같은 이름”으로 해야지 중복체크가 안됨.
- checkbox는 중복 선택 가능

### button vs input type=“button”

- input은 value로 text만 지정 가능하지만
- button은 닫는 태그가 있어 자식요소 등 더 다양하게 활용 가능

### 블록 요소 vs 인라인 요소

<p>블록 요소</p>
  <ul>
    <li>한 개의 덩어리. 사용하면 줄넘김이 됨</li>
    <li>요소 안의 길이와 상관 없음 - width, height 값 사용 가능</li>
    <li>대표적으로 article, header, section, div가 있음</li>
    <li><a href="https://developer.mozilla.org/ko/docs/Web/HTML/Block-level_elements" target="_blank"
        rel="noopener noreferrer">모든 block 요소들(MDN)</a></li>
  </ul>
  <p>인라인 요소</p>
  <ul>
    <li>자신의 크기만큼 영역을 가지는 요소</li>
    <li>인라인 요소끼리만 중첩이 가능. 전체 레이아웃의 영향을 받음 - width, height 값 사용 X, display: inline-block</li>
    <li>대표적으로 span, strong이 있음</li>
    <li><a href="https://developer.mozilla.org/ko/docs/Web/HTML/Inline_elements" target="_blank"
        rel="noopener noreferrer">모든 inline 요소들(MDN)</a></li>
  </ul>
  <p>과연.. 이걸 다 외워야 할까?ㅜ</p>
  <ul>
    <li>그래도 기본적인 속성은 알고있어야 더 효율적으로 문서 작성이 가능할 것이라는 생각</li>
    <li>하지만 이걸 다 외우는 건 무리같은데..ㅜㅜ</li>
    <li>수업 중 공유 받은 tag ranking -> <a href="advancedwebranking" target="_blank"
        rel="noopener noreferrer">advancedwebranking</a></li>
    <li>좋아!!! 여기 있는 것들만이라도 잘 익혀두자!!</li>
  </ul>
