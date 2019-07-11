​										Angular Form - Template driven

------

1.  submit 함수 연결은 <form></form>태그에 한다 

```
<form (ngSubmit)="onSubmit(f)" #f="ngForm">
```

2. <input>에는 ngModel을 달아주고 name을 준다.

```
<input
type="text"
id="username"
class="form-control"
ngModel
name="username"
required>
```

3. ngIf를 사용하려면 #email="ngModel"과 같이 해주면 attribute에 access 할 수 있다

```
<input #email="ngModel">
<span *ngIf="!email.valid && email.touched">
please enter a email valid</span>
         
```

4. ViewChild()를 이용해서 component에서도 활용 할 수 있다.

```
@ViewChild('f', { static: false }) signupForm: NgForm;

  onSubmit() {
    this.user.username = this.signupForm.value.userData.username;
    this.user.email = this.signupForm.value.userData.email;
    this.user.secret = this.signupForm.value.secret;
    this.signupForm.reset();
  }
```

