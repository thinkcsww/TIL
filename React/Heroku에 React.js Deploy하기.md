​	**Heroku Deploy - react.js**

------

<h2>Heroku에 React.js Deploy하기</h2>

// Buildpack 링크 : https://elements.heroku.com/buildpacks/mars/create-react-app-buildpack

<h2>Trouble Shooting</h2>

```
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```



<h5>1. Heroku cli를 설치한다</h5>

```
npm i -g heroku
```

// 홈페이지에 있는 brew로 하니까 안됨;;

<h5>2. Node.js 폴더에 가서 git init</h5>

```
rm -rf .git // 하기 전에 확실히 하기 위해서 깃 폴더를 초기화
git init
```

<h5>3. Git ingore에 node_modules 추가하기</h5>

```
touch node_modules > .gitignore
```

<h5>4. Heroku에 깃 레포지토리 만들기</h5>

```
heroku create $APP_NAME --buildpack mars/create-react-app
```

<h5>5. static.json 파일 만들기</h5>

```
touch static.json
//추가 해야 할 것들
{
    "root":"build/",
    "routes": {
        "/**": "index.html"
    },
    "proxies": {
        "/api": {
            "origin": "https://warbler-server-es2.herokuapp.com/api" // {서버 도메인/api}
        }
    }
}
```



```
git add.
git commit -m "message"
git push heroku master
```

