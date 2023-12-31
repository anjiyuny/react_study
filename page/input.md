---
description: input 태그 활용해 글 발행 기능 만들어보기
---

# 🧚 Input 활용해보기



### 😊 \<input> 태그 종류

```jsx
<input type="text"/>
<input type="range"/>
<input type="date"/>
<input type="number"/>
<textarea></textarea>
<select></select>
```

이 외에도 다양한 종류가 있으니 필요시 검색하여 찾아쓰면 된다.





### 😊 \<input> 입력시 코드 실행

```jsx
<input onChange={( )=>{ }}/>
```

유저가 \<input> 에 뭔가 입력시 코드를 실행해 주고싶으면

<mark style="background-color:yellow;">**onChange, onInput 라는 이벤트핸들러**</mark>를 쓸 수 있다.

(참고로 이벤트핸들러는 매우 다양하니 필요시 검색 하길....)





### 😊 \<input> 입력한 값 가져오기

```jsx
<input onChange={(e)=>{ console.log(e.target.value) }}/>
```

이벤트핸들러에 들어가는 함수에 파라미터 e 를 추가하면

<mark style="background-color:yellow;">**e는 이벤트 객체**</mark> 로서 현재 발생하는 이벤트와 관련한 유용한 기능들을 제공하는 일종의 변수가 된다.





### 😊 \<Input>에 입력한 데이터 저장하기

```jsx
function App (){

  let [입력값, 입력값변경] = useState('');
  return (
    <input onChange={(e)=>{ 
      입력값변경(e.target.value) 
      console.log(입력값)
    }} />
  )
}
```

사용자가 input에 입력한 데이터는 state 혹은 변수에 저장해서 쓰는게 일반적이다



(참고)

위 코드가 콘솔창에서 좀늦게 반응하는데&#x20;

그 이유는

<mark style="background-color:yellow;">**state 변경함수는 약간 늦게 처리된다고 한다.**</mark>&#x20;

<mark style="background-color:yellow;">**전문용어로 async(비동기적으로)처리된기 때문이라고 한다.**</mark>

자바스크립트에서는 늦게 처리되는 코드는 잠깐 제쳐두고 바로 다음줄을 먼저 실행한다고...





### ✏️ 숙제

1. input에 입력하고 버튼을 클릭하면 블로그에 글이 하나 추가 되는 기능 개발하기
2. 글마다 삭제 버튼 누르면 각 글이 삭제되는 기능 개발하기



#### ⬇️ 01. 글 추가 기능

```jsx
function App (){

  let [글제목, 글제목변경] = useState([
    "남자 코트 추천",
    "강남 우동 맛집",
    "파이썬 독학",
  ]);
  let [입력값, 입력값변경] = useState(''); // 새 타이틀을 받아올 스트링타입의 state 생성
  
  return (
   <div>
      <input  onChange={(e)=>{
        입력값변경(e.target.value);
      }}/>
      <button onClick={()=>{
        let copy = [...글제목, 입력값]; // 새로받아온 입력값에 복사한 글제목배열 복사해서 합침
        글제목변경(copy) // 위의 배열을 글제목배열에 추가
      }}>Enter</button>
   </div>
  )
}
```

이렇게 하면 문제는 상단에 글이 추가 되는것이 아니라 하단에 글이 추가 된다.



#### ⬇️ 01 - 1 글 추가 기능

```jsx
function App (){

  let [글제목, 글제목변경] = useState([
    "남자 코트 추천",
    "강남 우동 맛집",
    "파이썬 독학",
  ]);
  let [입력값, 입력값변경] = useState(''); // 새 타이틀을 받아올 스트링타입의 state 생성
  
  return (
   <div>
      <input  onChange={(e)=>{
        입력값변경(e.target.value); //사용자가 입력한 값을 배열로 state에 저장
      }}/>
      <button onClick={()=>{
        let copy = [...글제목]; //글제목 배열을 복사해줌
        copy.unshift(입력값);  // 입력한값을 복사한배열에 추가
        글제목변경(copy);     // state 변경함수 이용
      }}>Enter</button>
   </div>
  )
}
```

1. array 형태의 state 조작은 카피부터 하면 된다.
2. <mark style="background-color:yellow;">**arr.unshift ( '추가할자료' );**</mark>  <- 이것은 배열에 자료 추가하는 문법이다 알아놓자!
3. 그리고 state 변경함수를 이용!



#### ⬇️ 02 삭제 버튼 기능

```jsx
function App (){
  let [글제목, 글제목변경] = useState(['남자코트추천', '강남우동맛집', '파이썬독학']);
  let [입력값, 입력값변경] = useState('');
  return ( 
    <div>
    { 
     글제목.map(function(a, i){
        return (
          <div className="list">
            <h4>{ 글제목[i] }</h4>
            <p>2월 18일 발행</p>
            <button onClick={()=>{ 
              let copy = [...글제목];  //글제목 배열 사본만듬
              copy.splice(i, 1);    // i번째 자료를 삭제해준다
              글제목변경(copy);      // 삭제한자료로 state 변경해준다
           }}>삭제</button>
          </div> 
        )
     }) 
    }  
  </div>
  )
}
```

1. 먼저 array 형태의 state 조작은 카피부터 하면 된다.
2. <mark style="background-color:yellow;">**copy.splice(숫자, 1);**</mark>  <- 숫자 번째의 자료가 없어지는 문법!!

