---
description: 많은 div를 반복문으로 줄이고 싶을때
---

# 😀 Map 반복문



### 😊 map 함수 사용법



#### 01. map 기능

* array에 들어있는 자료갯수만큼 내부코드를 반복실행 해준다.

```jsx
var arr = [1,2,3]

arr.map(function(){
    console.log(1)
    // 1 이 세번 찍힘
});
```



#### 02. map 기능

* 콜백 함수 내의 파라미터는 array안에 모든 자료를 출력해준다

```jsx
var arr = [1,2,3]

arr.map(function(a){
    console.log(a)
    // 1,2,3 이 출력된다.
});
```



#### 03. map 기능

* return 오른쪽에 있는 내용은 array 로 담아준다.

```jsx
var arr = [1,2,3]

var newArr = arr.map(function(a){
    return a * 10
});

console.log(newArr);  // 10, 20, 30 출력됨
```





### 😊JSX안에서 HTML을 반복할 때



반복되는 div 3개를 축약해보자

"글제목" state도 array 이기 때문에 map함수를 사용할 수 있다.

```jsx
function App (){

  let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);

  return (
    <div>
      (생략)
      { 
        글제목.map(function(a , i){  // a,i 파라미터 추가
          return (
          <div className="list">
            <h4>{ 글제목[i] }</h4>// 혹은 a 만 써도 가능
            <p>2월 18일 발행</p>
          </div> )
        }) 
      }
    </div>
  )
}
```

&#x20;파라미터를 2개까지 작명 가능한데&#x20;

<mark style="background-color:yellow;">**첫째 파라미터 a는 array안에 있던 자료 ,둘째 파라미터 i는 0부터 1씩 증가하는 정수**</mark> 이다.



### ✏️ 숙제

클릭하면 따봉 숫자 올라가는 기능도 만들어 보자.



```jsx

function App() {

  let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);
  let [따봉,따봉변경] = useState([0,0,0]); 
  // 각각의 숫자를 담을 자리를 배열로 구성

  return (
    <div className="App">

        {
          글제목.map(function(a, i){
            return (
              <div className="list" key={i}>
              <h4> {글제목[i]} <span onClick={()=>{ 
                let copy = [...따봉]
                copy[i] = copy[i] + 1;
                따봉변경(copy);
              }}>👍</span> {따봉[i]} </h4>
              <p>2월 17일 발행</p>
            </div>
            )
          })
        }

    </div>
  )
}

```

state 를 수정할때 자료형이 array 이면 복사부터하고 수정해야하므로

독립적인 따봉 배열을 복사해서 copy에 넣어두고

copy\[i] 는 copy\[i] + 1 로 저장을 해주고

state 변경함수를 통해서 변경된 copy의 값으로 바꿔준다



그럼 클릭했을때 따봉의 값은 각각 따봉\[i]의 값으로 잘 올라가게 된다.





어쩐지 처음에&#x20;

```jsx
<span onClick={()=>{따봉변경(따봉[i] + 1)}}>👍</span> {따봉[i]} </h4>
```

이렇게 아무리 해도 바뀌질 않았다....
