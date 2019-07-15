												Angular HttpInterceptor

------

여러개의 interceptor 적용가능, 적은 순서대로 사용됨 

1. <이름-interceptor>.service.ts파일을 만든다.

2. HttpInterceptor를 implements한다.

3. 로직을 처리한다.

   1.  header에 정보 추가하기

   ```
   const modifiedRequest = req.clone({headers: req.headers.append('Auth', 'xyz')});
   ```

   2. 이벤트 타입에 따른 로직 처리와 전달 

   ```
   return next.handle(req).pipe(tap(event => {
         if (event.type === HttpEventType.Response) {
           console.log('Incoming response');
           console.log(event.body);
         }
       }))
   ```

4. app.module.ts에 providers[]에 다음과 같이 추가한다.

```
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule, HttpClientModule],
  providers: [
  // 여기서부터
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptorService,
      multi: true
    },
    {
      provide: HTTP_INTERCEPTORS,
      useClass: LogginInterceptorService,
      multi: true
    }
  ],
  bootstrap: [AppComponent]
})
```

