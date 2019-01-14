​								**Heroku Deploy - node.js**

------

<h2>Heroku에 Node.js Deploy하기</h2>



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
git init
```

<h5>3. Git ingore에 node_modules 추가하기</h5>

```
touch node_modules > .gitignore
//이걸 해야 Heroku에서 다시 모듈을 다운받아서 에러가 안생김
```

<h5>4. Heroku에 깃 레포지토리 만들기</h5>

```
heroku create <레포지토리 이름>
```

<h5>5. 깃 레포지토리 리모트 확인하기</h5>

```
git remote
```

<h5>6. Heroku에 mongolab 추가하기 </h5>

```
heroku addons:create mongolab // 이거 하려면 credit card 등록해야 하는데 다른 방법을 사용
```

/////////////

mLab에 가서 Database를 만든다 -> user를 만들고 주소를 Heroku config에 Key : MONGO_URL  Value: 주소

로 만든다.

서버의 index.js에서 mongo를 연결할 때 process.env.MONGO_URL을 사용한다.

끝 

<h5>7. Heroku에 env 변수 저장하기</h5>

```
heroku config:set <name>=<value>
```

<h5>8. Procfile 만들기</h5>

```
touch Procfile
//Procfile안에 
web: node index.js // 추가 -> Heroku에서 처음 index.js를 실행할 수 있게 만듬
```



```
git add.
git commit -m "message"
git push heroku master
```





