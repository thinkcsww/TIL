​																		Angular Obervable, Subject

------

Reactive 프로그래밍, Observable은 1개의 observer만 사용가능하고 Subject는 여러개가 가능하다?! 

Subject는 subscribe와 next를 다할 수 있다!? 

1. Subject를 생성한다. 

```
activatedEmitter = new Subject<boolean>();
```

2. Subject에서 next, error, complete를 사용해서 데이터를 스트림에 집어 넣는다.

```
this.userService.activatedEmitter.next(true);
```

3. Subscription을 만들어서 stream을 observe한다.

```
this.activatedSub = this.userService.activatedEmitter.subscribe(didActivate => {
      this.userActivated = didActivate;
    })
```

4. pipe를 통해서 데이터를 가공한다. 

```
this.firstObsSubscription = this.userService.activatedEmitter.pipe(filter((data) => {
      return data > 0;
    }),map(data => {
      return 'Round: ' + (+data + 1);
    })).subscribe(data => {
      console.log(data);
    }, error => {
      console.log(error);
      alert(error.message);
    }, () => {
      console.log('Completed!');
    });
  }
```

5. 메모리 활용을 위해 unsubscribe를 한다 .

```
ngOnDestroy(): void {
    this.userService.activatedEmitter.unsubscribe();
}
```

