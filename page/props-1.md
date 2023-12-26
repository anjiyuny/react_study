# 🌳 Props 응용편

### ✏️ Props 응용 문제

* 제목을 누르면 모달창에도 제목이 나타나게끔 기능 개발을 해보자!



그전에!!  <mark style="background-color:orange;">**동적인 UI를 만드는 원리**</mark>를 기억해야한다.

1. html, css로 미리 완성된 디자인을 해놓는다.
2. 현재 UI의 상태를 state로 저장해 놓는다
3. state 종류에 따라서 UI가 어떻게 보일지 작성한다.



### ☝️ STEP 01

: html, css로 미리 완성된 디자인을 해놓는다.

{% code title="기존 코드" %}
```jsx

import { useState } from "react";
import "./App.css";

function App() {

  let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);
  let [logo , setLogo] = useState('ReactBlog');
  let [따봉,따봉변경] = useState([0,0,0]);
  let[modal, setModal] = useState(false);
  
  return (
    <div className="App">
      <div className="black-nav">
        <h4 style = {{color:'red',fontSize:'16px'}}>{logo}</h4>
      </div>
      
      {
        글제목.map(function(a,i){
          return(
            <div className="list" key={i}>
            <h4 onClick={()=>{setModal(true);}}>{글제목[i]} 
            <span onClick={()=>{
              let copy = [...따봉]
              copy[i] = copy[i] + 1
              따봉변경(copy)
            }}>👍</span>{따봉[i]}</h4>
            <p>2월 17일 발행</p>
          </div>
          )
        })
      }

      {modal == true ? <Modal 글제목 = {글제목} 글제목변경 = {글제목변경}/> : null}
      {/* modal이 true면 모달창 띄우고 아님 비워라 */}
    </div>
  )
}

// 모달창 코드
function Modal(props){
  return(
    <div className="modal">
      <h4>목</h4>
      <p>날짜</p>
      <p>상세내용</p>
      <button onClick={()=>{}}>글수정</button> 
    </div>
  )
}

export default App;

```
{% endcode %}





### ✌️STEP 02

: 현재 UI의 상태를 state로 저장해 놓는다

```jsx
let [title, setTitle] = useState(0); // 추가한 state
```

function Modal 안의 h4를 title로 작명해 현재 state에 0 이라는 상태로 저장을 해놓음

0으로 한 이유는 클릭을 할때 마다 숫자가 바뀌면서 state가 스위치 역할을 해아하는데

true or false 로 하면 상태변환이 두개뿐이라 적절하지 않다..





### 👌STEP 03

: state 종류에 따라서 UI가 어떻게 보일지 작성한다.

```jsx
function App (){
  let [title, setTitle] = useState(0);
  {
    글제목.map(function(a,i){
      return(
        <div className="list" key={i}>
        <h4 onClick={()=>{setModal(true); setTitle(i)}}>{글제목[i]} 
        // 클릭할때마다 title의 숫자가 각 제목의 인덱스 숫자로 바뀐다
        <span onClick={()=>{
          let copy = [...따봉]
          copy[i] = copy[i] + 1
          따봉변경(copy)
        }}>👍</span>{따봉[i]}</h4>
        <p>2월 17일 발행</p>
      </div>
      )
    })
  }

  {modal == true ? <Modal 글제목 = {글제목} title = {title}/> : null}
}

function Modal(props){
  return (
    <div className="modal">
      <h4>{props.글제목[props.title]}</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```
