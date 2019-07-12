​															Angular form reactive validator

------

Reactive Form에서 Validator 사용 방법

1.  Validator는 FormControl의 2번째 파라미터부터 계속해서 사용할 수 있다.

```
this.signupForm = new FormGroup({
      'userData': new FormGroup({
        'username': new FormControl(null, [Validators.required),
        'email': new FormControl(null, [Validators.required, Validators.email]),
      }),
      'gender': new FormControl('male'),
      'hobbies': new FormArray([])
    });
```

2. Custom validator도 같은 방법으로 사용할 수 있다.

Custom validator 정의

```
forbiddenNames(control: FormControl): {[s: string]: boolean} {
    if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
      return {'nameIsForbidden': true};
    }
    return null;
  }
```



Custom validator 사용 

```
FormControl(null, [Validators.required, this.forbiddenNames.bind(this)])
```



3. Async Custom validator는 3번째 파라미터에 사용할 수 있다.

Custom async validator 정의

```
forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
    const promise = new Promise<any>((resolve, reject) => {
      setTimeout(() => {
        if (control.value === 'test@test.com') {
          resolve({'emailIsForbidden': true})
        } else {
          resolve(null);
        }
      }, 1500);
    });
    return promise;
  }
```



Custom async validator 사용

```
FormControl(null, [Validators.required, Validators.email], this.forbiddenEmails)
```