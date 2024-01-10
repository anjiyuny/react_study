---
description: 코드가 길어질때 사용할 수 있는 import export!
---

# 😄 import & export



### 😊 export default / import 문법

state안에 저장하고 싶은 자료가 있는데 너무\~ 길다면 다른 파일에 보관했다가 꺼내쓸 수 있다.



#### ⬇️ export default 변수명;&#x20;

이렇게 쓰면 원하는 변수를 밖으로 내보낼 수 있다.

{% code title="data.js 파일" %}
```javascript
let a  = 10 ;
export default a;
```
{% endcode %}

#### ⬇️ **import 작명 from './파일경로'**&#x20;

{% code title="App.js 파일" %}
```jsx
import a from './data.js';
console.log(a); 
// 10출력
```
{% endcode %}

