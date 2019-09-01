​																	Angular NgRx Effects

------

Effects는 dispatch된 action에 따라서 대응할 수 있게 해주는 방법이다. 예를 들어 서버에 http 통신으로 로그인을 할 때 단계를

로그인 시작, 로그인 완료, 로그인 실패로 나눈다면

로그인이 시작 되었을 때, 완료 되었을 때, 실패했을 때  대응을 하는 로직을 구현할 수 있고 구현할 수 있다. 

예를 들면, 다음과 같이 LoginStart Action을 dispatch하면

```
this.store.dispatch(new AuthActions.LoginStart({email: email, password: password}));
```

다음과 같이 effect에서 받아서 http 통신을 날리고 실패했을때 LoginFail을 Dispatch한다.

반드시 Observable을 return 해야한다. 그래야 effect가 볼 수 있기 때문? NgRx쓰기 때문?

dispatch 함수가 따로 없는 이유는 Observable을 return하면 자동으로 effect가 dispatch 해주기 때문이다.

또한  of() 함수를 쓰는 이유는 catchError에서 return을 하면 Observable을 return하지 않기 때문이고, 

throwError를 날리면 상위의 effect Observable(어떤 action이 들어오나 관찰하는)이 죽기 때문에 날리지 않고  LoginFail과 같은 Observable을 return 한다.

```
@Effect()
  authLogin = this.actions$.pipe(
  	// 어떤 type인지 구별하는 곳
    ofType(AuthActions.LOGIN_START),
    switchMap((authData: AuthActions.LoginStart) => {
      return this.http
        .post<AuthResponseData>(
          'https://www.googleapis.com/identitytoolkit/v3/relyingparty/verifyPassword?key=AIzaSyA6LQDRF9W-fCQQETLaAKYk7t8OF7PclkQ',
          {
            email: authData.payload.email,
            password: authData.payload.password,
            returnSecureToken: true
          }
        ).pipe(
          map(resData => {
            const expirationDate = new Date(new Date().getTime() + +resData.expiresIn * 1000);
            return new AuthActions.Login({
              email: resData.email, userId: resData.localId, token: resData.idToken, expirationDate: expirationDate
            });
          }),
          catchError(errorRes => {
            let errorMessage = 'An unknown error occurred!';
            if (!errorRes.error || !errorRes.error.error) {
              return of(new AuthActions.LoginFail(errorMessage));
            }
            switch (errorRes.error.error.message) {
              case 'EMAIL_EXISTS':
                errorMessage = 'This email exists already';
                break;
              case 'EMAIL_NOT_FOUND':
                errorMessage = 'This email does not exist.';
                break;
              case 'INVALID_PASSWORD':
                errorMessage = 'This password is not correct.';
                break;
            }
            return of(new AuthActions.LoginFail(errorMessage));
          }),
        )
        ;
    }),
  );
```

