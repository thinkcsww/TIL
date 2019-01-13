​										**body-parser**

------

body-parser는 http post request에서 body 부분 즉, 실질적인 데이터 부분을 사용할 수 있게 바꿔주는 Node.js 모듈이다.

**사용방법**

```
npm install body-parser

const bodyParser = require('body-parser');

app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: true }))
```

