​									 Angular param route로 통신하기 (GET 비슷)

------

1. app.module.ts에 route를 설정해준다. 

```
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'users/:id/:name', component: UserComponent },
  { path: 'servers', component: ServersComponent },
];
```

2. 템플릿에서 보내는 방법 

```
<a 
	[routerLink]="['/users', 10, 'Anna']"
	[queryParams]="{name: 'mary', age: '20'}
	fragment="hello">asdf</a>
```

이렇게 보내면 "your_home/users/10/Anna?name='mary'&age='20'#hello" 이렇게 온다.

3. 컴포넌트에서 보내는 방법은 Router 객체를 사용해서 비슷한 방법으로 보낸다.

```
 ...
 constructor(private router: Router) { }

  ngOnInit() {
  }

  onLoadServer(id: number) {
    this.router.
    navigate(
      ['/servers', id, 'edit'], 
      {queryParams: {allowEdit: '1'},
      fragment: 'loading'}
    );
  }
```



4. 컴포넌트에서 받는 방법은 ActivatedRoute를 inject 한 후 받으면 된다.

```
...
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    this.user = {
      id: this.route.snapshot.params['id'],
      name: this.route.snapshot.params['name'],
    }
  }
}
```

5. Rxjs를 써서 받는 방법은 다음과 같다. (Observable)

```
export class UserComponent implements OnInit {
  user: {id: number, name: string};
	paramSubscription: Subscription;
	
  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
  	this.paramSubscription = this.route.params
    	.subscribe(
    		(params: Params) => {
    			this.user.id = params['id'];
    			this.user.name = params['name'];
    		}
    	)
  }
  
  ngOnDestroy() {
  	this.paramSubscription.unsubscribe();
  }
}
```