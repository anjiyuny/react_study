# 👩💻 리액트 : 라우터 설치하기

### 😊 react-router-dom 설치하기



1. 터미널 열어서 **npm install react-router-dom@6** 입력하기
2. index.js 파일로 이동후 셋팅 하는데 방법은 아래 참고

```jsx
import { BrowserRouter } from "react-router-dom"; // import 해오기

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
      <BrowserRouter>
        <App />
      </BrowserRouter>
  </React.StrictMode>
); 
```





### 😊 router 사용해보기



웹사이트의 주소를 자세히 살펴보면

**google.com/ 어쩌구A** 로 접속하면 A 페이지를 보여주고

**google.com/ 어쩌구B** 로 접속하면  B 페이지를 보여준다.

<mark style="background-color:yellow;">**url 경로마다 다른 페이지를 보여주고 싶을때 라우터를 사용해주면 된다.**</mark>



{% code title="App.js 파일" %}
```jsx
import { Routes, Route, Link } from 'react-router-dom';

function App(){
  return (
    (생략)
    <Routes>
      <Route path="/detail" element={ <div>상세페이지임</div> } />
      <Route path="/about" element={ <div>어바웃페이지임</div> } />
    </Routes>
  )
}
```
{% endcode %}

1. 상단에 필요한 여러가지 컴포넌트를 import 해온다.
2. \<Routes>안에 \<Route>를 만든다.
3. \<Route path="/url경로" element={ <보여줄html> } /> 를 작성한다.

이렇게 하면 **"main주소/detail.com", "main주소/about.com"** 경로로 페이지가 생성된다.





### ⬇️  메인페이지 경로

```jsx
<Route path="/" element={ <div>메인페이지에서 보여줄거</div> } /> 
```

이 경로는 메인페이지 경로이다.

메인 페이지에 보여줄 html 내용을 저기 element 안에 넣으면 된다.





### ☝️참고 :   페이지 이동 버튼

```jsx
<Link to="/">홈</Link>
<Link to="/detail">상세페이지</Link>
```

해당 경로로 이동하는 링크를 생성 할 수 있다.





### ✏️ 숙제

detail 로 접속하면 보여줄 상세페이지를 컴포넌트를 이용해서 만들어 보기

{% code title="Detail.js 파일" %}
```javascript
function Detail() {
  return (
    <div className="container">
      <div className="row">
        <div className="col-md-6">
          <img
            src="https://codingapple1.github.io/shop/shoes1.jpg"
            width="100%"
          />
        </div>
        <div className="col-md-6">
          <h4 className="pt-5">상품명</h4>
          <p>상품설명</p>
          <p>120000원</p>
          <button className="btn btn-danger">주문하기</button>
        </div>
      </div>
    </div>
  );
}
export default Detail;
// 컴포넌트는대문자...기억하자...
```
{% endcode %}



{% code title="App.js 파일" %}
```jsx
import Detail from './routes/Detail.js';

function App() {
  let [shoes] = useState(data);
  let navigate = useNavigate(); // 페이지 이동 도와줌

  return (
    <div className="App">
      <Routes>  
        {/* 상세페이지 */}
          <Route path="/detail" element={<Detail/>}>
        </Route>
        
        {/* 404 */}
        <Route path="*" element={<div>없는 페이짐 돌아가셈</div>}></Route>
        
        {/* about */}
        <Route path="/about" element={<About/>}> 
          <Route path="member" element={<div>멤버임</div>}/>{/* nasted routes */}
          <Route path="location" element={<div>위치정보임</div>}/>
        </Route>
    </Routes>
    </div>
  );
}
```
{% endcode %}
