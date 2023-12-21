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



#### ⚠️참고사항⚠️&#x20;

* &#x20;props는 **\<Modal 이런거={이런거}  저런거={저런거}>** 이렇게 무한히 전송이 가능하다.
* state 뿐만 아니라 변수, 함수도 전송이 가능하고 일반문자는 중괄호 없이 전송 가능하다.
* 자식 -> 부모 방향으로 전송은 불가능하다
* 자식 끼리의 전송 또한 불가능하다.





### 😊 props는 함수 파라미터와 똑같다

함수 하나로 다양한 기능을 사용하기 위해서 쓰는것이 파라미터 문법인데,

실은 props도 파라미터랑 똑같은 문법이다.



⬇️ 하늘색 배경이 필요할때

```jsx
function Modal(props){
  return (
    <div className="modal" style={{ background : 'skyblue' }}>
      <h4>{ props.글제목[0] }</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```

모달 배경에 하늘색이 필요하다면 위 와 같이 직접적으로 스타일을 입힐 수 있다.

여러색의 배경이 필요하다면&#x20;

function Modal1(){}, function Modal2()}{}.... 이렇게 여러 컴포넌트를 만들수 있다.



하지만!



props 를 활용한다면 코드가 훨신 간단해 진다.

<pre class="language-jsx"><code class="lang-jsx">function App (){
  return (
    &#x3C;div className="App">
      &#x3C;Modal color={'orange'}>&#x3C;/Modal>
      // &#x3C;Modal color={'skyblue'}>&#x3C;/Modal>
    &#x3C;/div>
  )
}
<strong>
</strong><strong>function Modal(props){
</strong>  return (
    &#x3C;div className="modal" style={{ background : props.color }}>
      &#x3C;h4>{ props.글제목[0] }&#x3C;/h4>
      &#x3C;p>날짜&#x3C;/p>
      &#x3C;p>상세내용&#x3C;/p>
    &#x3C;/div>
  )
}
</code></pre>

props.color 로 자리를 만들어 놓고 컴포넌트를 사용할때

\<Modal color={'skyblue'} /> 이렇게 컬러를 바꿔주면 해당 컬러가 props작명 자리로 들어가서

색상이 바뀌게 된다!!





### ✏️ 숙제

모달창안에 글수정버튼 만들고

그거 누르면 첫 글제목이 '여자코트 추천'으로 바뀌는 기능을 만들어봅시다.



```jsx
function App (){
  let [글제목, 글제목변경] = useState(['남자코트 추천', '강남 우동맛집', '파이썬독학']);
  return (
    <div className="App">
      {
        modal == true ? <Modal 글제목 = {글제목} 글제목변경 = {글제목변경}/> : null
      }
      // 글제목, 글제목변경 state를 가져옴
    </div>
  )
}


function Modal(props){
  return(
    <div className="modal">
      <h4>{props.글제목[0]}</h4>
      <p>날짜</p>
      <p>상세내용</p>
      <button onClick={()=>{
        let copy = [...props.글제목] //글제목배열을 복사
        copy[0]='여자 코트 추천';    // 복사한것의 첫번째 문자를 변경
        props.글제목변경(copy);     // 변경함수를 사용해 바꾼 값 넣어줌
      }}>글수정</button> 
    </div>
  )
}

```



[^1]: 이렇게 수정하면 에러 난다.
