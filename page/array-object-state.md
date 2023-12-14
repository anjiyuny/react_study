---
description: state에 저장된 자료가 array / object일 경우 state를 어떻게 수정하는지 알아보자
---

# 🤓 array/object state 변경하기



지난번 숙제로 버튼을 누르면 글 제목이 바뀌는 기능을 개발해 보았는데

```jsx
function App(){
  
  let [글제목, 글제목변경] = useState( ['남자코트 추천', '강남 우동맛집', '파이썬 독학'] );  
  
  return (
    <button onClick={ ()=>{ 
      글제목변경(['여자코트 추천', '강남 우동맛집', '파이썬 독학'])
    } }> 수정버튼 </button>
  )
}

```

이렇게 해도 기능에 이상은 없지만,

&#x20;만약 array 자료가 100개가 넘는다면... 모두 다 이런식으로 수정을 할 수는 없기 때문에&#x20;

오늘은 새로운 방법을 알아본다.





### ✅ state 변경함수 특징

먼저 state 변경함수의 특징 부터 알아보자면

<mark style="background-color:yellow;">**기존 state 와 변경 state가 동일하면 변경해주지 않는다**</mark>





### ✅ array/object 특징

```jsx
let arr = [1,2,3];
```

위 와 같은 경우에 array / object를 담은 변수엔 \[1,2,3]이 어디있는지 알려주는 **화살표만 저장된다.**



동작 원리를 간단히 살펴보자면

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

\[1,2,3] 자료는 램이라는 가상공간에 몰래 저장이 되고

let arr 변수엔 그 자료가 어디있는지 가리키는 **화살표만 담겨있다.**



▼ array / object 를 복사하게 되면!

```jsx
let data1 = [1,2,3];
let data2 = data1;   //복사문법임 
```

data2 를 출력하면 \[1,2,3] 이 출력된다.

근데 data1 과 data2는 각각의 \[1,2,3]을 별개로 저장하는것이 아니라

<mark style="background-color:yellow;">**data1 과 data2는 똑같은 값을 공유하는 것**</mark>이다.





### 😀 state  변경하기



#### ⬇️ 방법 01

```jsx
function App(){
    return(
        let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);
          <button onClick={()=>{
            글제목[0] = '여자 코트 추천';
            글제목변경(글제목)
          }}>글제목 바꾸기</button>
    )
}
```

이렇게 하면 안되는 이유는&#x20;

글제목에 저장되어있던 화살표는 바뀐적이 없기 때문에&#x20;

기존state 와 신규state 가 같다고 판단해서 변경이 안되는 것이다.



#### ⬇️ 방법 02

```jsx
function App(){
    return(
        let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);
          <button onClick={()=>{
              let copy = 글제목;
              copy[0]='여자 코트 추천';
              글제목변경(copy);
          }}>글제목 바꾸기</button>
    )
}
```

글제목 이라는 변수에 저장되어있는건 array 자료가 아니라 화살표만 저장이 되어있는 것이기 때문에

이 방법도 동작하지 않는다



#### ⬇️ 정답

```jsx
let copy = [...글제목];
copy[0] = '여자코트 추천';
글제목변경(copy)
```

리액트에서 array/object state를 수정하고 싶으면 독립적인 카피본을 만들어서 수정하는게 좋다고 한다.

\[...기존state] {...기존state}&#x20;

이렇게 하면 독립적인 카피가 하나 생성된다고 한다!!!!





### ✏️ 숙제

숙제 가나다순정렬 버튼 기능 개발 해보기

```jsx
function App(){
    return(
        let [글제목 ,글제목변경] = useState(['남자 코트 추천', '강남 우동 맛집', '파이썬 독학']);
            <button onClick={()=>{
              let copy = [...글제목];
              글제목변경(copy.sort());
            }}>가나다순정렬</button>
    )
}
```

독립적인 카피본을 생성해주고 그 배열을 내림차순으로 정렬 시켰다...!
