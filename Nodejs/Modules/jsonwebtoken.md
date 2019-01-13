​										**jsonwebtoken**

------

jwt는 웹 토큰으로 인증에 사용된다. jwt를 사용하면 서버가 클라이언트에게 요청을 받을 때 마다 해당 토큰이 유효하고 인증되었는지 확인하면 되기 때문에 세션을 유지할 필요가 없어서 서버 자원을 많이 아낄 수 있다.  

그리고 정보 교류에 있어서 정보가 sign이 되어 있기 때문에 중간에 정보가 변형되지 않았는지 검증할 수 있다.



jwt는 .을 경계로 header.payload.signature 형식의 문자열로 이루어져있다.



<h2>헤더(Header)</h2>

Typ: 토큰의 타입 -> JWT 토큰

alg: 해싱에 사용 할 알고리즘



```
{
    "typ": "JWT",
    "alg": "HS256"
}
```





<h2>정보(Payload)</h2>

Payload에는 토큰에 담을 정보가 담겨있다. 담긴 정보의 한 조각을 **Claim**이라고 부르고 name : value의 한 쌍으로 이뤄져 있고 토큰에는 여러개의 **Claim** 을 담을 수 있다

클레임의 종류는 registered, public, private 세가지가 있다. 

<h3>registered</h3>

등록된 클레임은 토큰에 대한 정보를 담기 위해 이미 정해진 클레임이다. 토큰 발급자(iss), 토큰제목(sub) 등이 있다. 

이것은 사용자의 필요에 따라 사용한다. 



**예시**

```
{
    "iss": "velopert.com",
    "exp": "1485270000000",
    "https://velopert.com/jwt_claims/is_admin": true,
    "userId": "11028373727102",
    "username": "velopert"
}
```



<h3>public</h3>

공개 클레임들은 유니크한 이름을 갖고, 이를 위해서 URI 형식으로 짓는다.

```
"https://velopert.com/jwt_claims/is_admin": true
```



<h3>private</h3>

비공개 클레임은 서버, 클라이언트 간에 협의하에 사용되는 클레임 이름들이다. 공개 클레임과는 달리 유니크하지 않기에 사용할 때 유의해야 한다.





<h2>서명(signature)</h2>



JWT의 마지막 부분은 서명이다. 이 서명은 헤더의 인코딩 값과 정보의 인코딩 값을 합친 후 주어진 비밀키로 해시를 하여 생성 된다.



**사용방법**

```
npm install jsonwebtoken;

const jwt = require('jsonwebtoken');

// sign 함수 안에 주어지는 값에 따라서 토큰을 다르게 부여한다.
let token = jwt.sign({
    id,
    username,
    etc
// process.env.SECRET_KEY는 개발자가 부여할 수 있는데 이 키에 따라서 signature가 바뀐다
}, process.env.SECRET_KEY)
```

