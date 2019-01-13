​											**Cors**

------

Cors는 로컬에서 프론트, 백엔드 서버를 동시에 돌리면 보안상 불가능한데 이것을 우회하게 해주는 모듈이다.

사용방법

```
npm install cors

const cors = require('cors');

app.use(cors())
```

