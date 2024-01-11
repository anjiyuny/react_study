---
description: 코드가 길어질때 사용할 수 있는 import export!
---

# 😄 import & export



### 😊 export default / import 문법

state안에 저장하고 싶은 자료가 있는데 너무\~ 길다면 다른 파일에 보관했다가 꺼내  쓸 수 있다.



#### ⬇️ export default 변수명;&#x20;

이렇게 쓰면 원하는 변수를 밖으로 내보낼 수 있다.

{% code title="data.js 파일" %}
```javascript
let a  = 10 ;
export default a;
```
{% endcode %}

#### ⬇️ **import 작명 from './파일경로'**&#x20;

export했던 변수를 다른 파일로 사용할 수 있다.

{% code title="App.js 파일" %}
```jsx
import a from './data.js';
console.log(a); 
// 10출력
```
{% endcode %}

#### ⬇️ 보낼 자료가 여러개인 경우

{% code title="data.js 파일" %}
```javascript
var name1 = 'Kim';
var name2 = 'Park';
export { name1, name2 }
```
{% endcode %}

{% code title="App.js 파일" %}
```jsx
import { name1, name2 } from './data.js';
```
{% endcode %}

* export { } 로 내보냈다면 import { } 로 가져와야한다
* 보낼자료가 여러 개인 경우에는 import 할 때 자유 작명이 불가능 하다.
* 파일마다 export default 라는 키워드는 하나만 사용 가능하다.

