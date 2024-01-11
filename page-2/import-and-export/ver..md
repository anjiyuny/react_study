# ☑ 강의 정답 ver.

### 😊 data.js

```javascript

let data = [
  {
    id: 0,
    title: "White and Black",
    content: "Born in France",
    price: 120000,
  },

  {
    id: 1,
    title: "Red Knit",
    content: "Born in Seoul",
    price: 110000,
  },

  {
    id: 2,
    title: "Grey Yordan",
    content: "Born in the States",
    price: 130000,
  },
];
export default data;

```

데이터 내보내기 완





### 😊 App.js

```jsx

import "./App.css";
import { useState } from "react";

import Container from "react-bootstrap/Container";
import Nav from "react-bootstrap/Nav";
import Navbar from "react-bootstrap/Navbar";
import Row from 'react-bootstrap/Row';
import Col from 'react-bootstrap/Col';
// 이미지 넣는법
import mBg from './images/main_bg.png';
// data 가져오기
import data from "./data";


function App() {
  let [shoes] = useState(data);
  return (
    <div className="App">
      <Navbar bg="dark" data-bs-theme="dark">
        <Container>
          <Navbar.Brand href="#home">Navbar</Navbar.Brand>
          <Nav className="me-auto">
            <Nav.Link href="#home">Home</Nav.Link>
            <Nav.Link href="#features">Features</Nav.Link>
            <Nav.Link href="#pricing">Pricing</Nav.Link>
          </Nav>
        </Container>
      </Navbar>

      <div className="main_bg" style={{backgroundImage:'url('+ mBg +')'}}></div>
      
      <Container>
        <Row>
          <Card shoes={shoes[0]} i= {1}/> {/*0번째 데이터만 전송*/}
          <Card shoes={shoes[1]} i ={2}/>
          <Card shoes={shoes[2]} i ={3}/>
        </Row>
    </Container>
    </div>
  );
}
//Card 컴포넌트
function Card(props){
  return(
    <div className="card">
        <Col>
          <img src={'https://codingapple1.github.io/shop/shoes'+ props.i +'.jpg'} width={'80+%+'}/>
          <h4>{props.shoes.title}</h4>
          <p>{props.shoes.price}</p>
      </Col>
    </div>
  )
}

export default data;

```

