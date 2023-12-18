---
description: 많은 div를 줄이고 싶다면 component를 만들어 사용할 수 있다.
---

# ☺ Component 만들어 사용하기



### 😊 Component 만드는 방법

Component를 이용하면 함수 혹은 변수를 만드는 것처럼 HTML을   한 단어로 치환해서 원하는 곳에 넣을 수 있다고 한다



1. <mark style="background-color:yellow;">**function 을 이용해서 함수 하나 만들고 작명 하기**</mark>
2. <mark style="background-color:yellow;">**그 함수 안 return( ) 안에 축약하고자 하는 html 담기**</mark>
3. <mark style="background-color:yellow;">**원하는 곳에 <함수명> \</함수명> 사용하면 축약한 HTML이 등장한다.**</mark>



```jsx
function App (){
  return (
    <div>
      (생략)
      <Modal></Modal>
    </div>
  )
}

function Modal(){
  return (
    <div className="modal">
      <h4>제목</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```





### 😊 Component 만들 때 주의점

1. Component 작명할 때 영어대문자로 보통 작명한다.
2. return() 안에 html 태그들이 평행하게 여러개 들어갈 수 없다.
3. function App( ){ } 내부에 component를 만들수 없다.
4. <컴포넌트>\</컴포넌트> 혹은 <컴포넌트/> 라고 사용할 수 있다.





### 😊 Arrow function 가능하다

```jsx
function Modal(){
  return ( <div></div> )
}

let Modal = () => {
  return ( <div></div>) 
}

function Modal(){
  return(
    <div></div>
  )
}
```

위의 세가지 방법 모두 가능하다.





### &#x20;😊Component 사용하는 상황

1. 사이트에서 반복해서 출현하는 HTML 덩어리들은 Component 로 만들어 준다.
2. 내용이 자주 변경될 것 같은 HTML 부분을 잘라서 Component 로 만들면 좋다.
3. 다른 페이지를 만들때 그 페이지의 HTML 내용을 하나의 Component로 만든다.
4. 다른 팀원과 협업할 때 웹페이지를 Component 단위로 나눠서 작업을 분배하기도 한다.



