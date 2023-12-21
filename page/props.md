---
description: 자식컴포넌트에서 부모컴포넌트 state 를 가져다 쓰고 싶을때
---

# 🍀 Props



자식컴포넌트에서 부모컴포넌트의 state를 사용해야 한다면 어떻게 해야할까?



#### ⬇️ **기존의 modal 컴포넌트**

<pre class="language-jsx"><code class="lang-jsx">function App (){
let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬독학']);
  return (
    &#x3C;div>
      (생략)
      &#x3C;Modal>&#x3C;/Modal>
    &#x3C;/div>
  )
}

function Modal(){
  return (
    &#x3C;div className="modal">
      <a data-footnote-ref href="#user-content-fn-1">&#x3C;h4>제목&#x3C;/h4> --------> &#x3C;h4>{ 글제목[0] }&#x3C;/h4> ???????</a>
      &#x3C;p>날짜&#x3C;/p>
      &#x3C;p>상세내용&#x3C;/p>
    &#x3C;/div>
  )
}
</code></pre>

위 와 같은 방법으로는 에러만 날뿐이다.





### 😊 props로 state 전송하는 방법

1. **자식컴포넌트 사용하는 곳에 가서 **<mark style="background-color:yellow;">**<자식컴포넌트 작명={state이름} />**</mark>&#x20;
2. &#x20;**자식컴포넌트 만드는 function으로 가서 props라는 파라미터 등록 후 **<mark style="background-color:yellow;">**props.작명**</mark>** 사용**



```jsx
function App (){
  let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬독학']);
  return (
    <div>
      <Modal 글제목={글제목}></Modal>
    </div>
  )
}

function Modal(props){
  return (
    <div className="modal">
      <h4>{ props.글제목[0] }</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```

[^1]: 이렇게 수정하면 에러 난다.
