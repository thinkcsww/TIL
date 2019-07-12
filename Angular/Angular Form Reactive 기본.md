​															Angular Form Reactive 기본

------

Template driven보다 더 정교한 작업을 할 수 있다.

1. app.module.ts에 ReactiveFormsModule을 추가한다.



1. 컴포넌트 파일에 form을 연결해주는 객체를 선언한다.

```
signupForm: FormGroup;
```



3. onInit()에서 form의 구조를 선언한다. 
   FormGroup은 Nested 구조로 사용될 수 있고, input, select, radio 등의 태그들은 FormControl 객체로 연결한다.

   FormControl에서 null이 아닌 값을 주면 초기화 된다.

```
this.signupForm = new FormGroup({
      'userData': new FormGroup({
        'username': new FormControl(null),
        'email': new FormControl(null),
      }),
      'gender': new FormControl('male'),
      'hobbies': new FormArray([])
    });
```



4. 다음과 같은 방법으로도 초기화 할 수 있다.

```
this.signupForm.setValue({
      'userData': {
        'username': 'Max',
        'email': 'max@test.com'
      },
      'gender': 'male',
      'hobbies': [],
    })
```



4. 템플릿 파일에서 연결해준다. 
   FormGroup, FormControlName

```
<form [formGroup]="signupForm" (ngSubmit)="onSubmit()"> formgroup level: 1
	<div formGroupName="userData"> // nested formgroup level: 2 
    <div class="form-group">
    <label for="username">Username</label>
      <input
      type="text"
      id="username"
      class="form-control"
      formControlName="username">
    </div>
    <div class="form-group">
      <label for="email">email</label>
      <input
      type="text"
      id="email"
      formControlName="email"
      class="form-control">
    </div>
  </div>
</form>
```

