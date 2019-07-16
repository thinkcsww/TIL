​														Angular 자동 로그인 using token

------

Token과 local storage를 사용한 자동로그인

유저 모델 - token이 exipire 되면 token을 반환하지 않는 로직이 꼭 필요!

```
export class User {
  constructor(
    public email: string,
    public id: string,
    private _token: string,
    private _tokenExpiration: Date
  ) {}

  get token() {
    if (new Date() > this._tokenExpiration || !this._tokenExpiration) {
      return null;
    }
    return this._token;
  }
}

```



1. 로그인 할 때 local storage에 토큰을 가진 user 객체를 stringify해서 저장한다. 정확하게는 pipe를 사용해서 

```
  signup(email: string, password: string) {
    return this.http.post<AuthResponseData>('https://www.googleapis.com/identitytoolkit/v3/relyingparty/signupNewUser?key=AIzaSyA6LQDRF9W-fCQQETLaAKYk7t8OF7PclkQ',
      {
        email: email,
        password: password,
        returnSecureToken: true
      }
    ).pipe(
      catchError(this.handleError),
      tap(responseData => {
        this.handleAuthentication(responseData.email, responseData.localId, responseData.idToken, +responseData.expiresIn,);
      })
    )
  }
```



```
private handleAuthentication(email: string, userId: string, token: string, expiresIn: number) {
    const expirationDate = new Date(new Date().getTime() + expiresIn * 1000);
    const user = new User(email, userId, token, expirationDate);
    this.user.next(user);
    localStorage.setItem('userData', JSON.stringify(user));
  }
```



2. autoLogin() 함수를 만든다. localStorage에 저장된 stringify된 객체를 불러와서 사용한다. 

```
autoLogin() {
    const userData: {
      email: string;
      id: string;
      _token: string;
      _tokenExpirationDate: string;
    } = JSON.parse(localStorage.getItem('userData'));
    if (!userData) {
      return;
    }

    const loadedUser = new User(userData.email, userData.id, userData._token, new Date(userData._tokenExpirationDate));

    if (loadedUser.token) {
      this.user.next(loadedUser);
    }
  }
```



3. app.component.ts에서 ngOnInit에 사용한다.

```
...
export class AppComponent implements OnInit{
  constructor(private authService: AuthService) {}

  ngOnInit(): void {
    this.authService.autoLogin();
  }
}
```

