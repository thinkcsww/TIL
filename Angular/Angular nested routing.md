​									Angular nested routing

------

1. children attribute에 배열로 path들을 넣는다.

```
const appRoutes: Routes = [
  { path: 'users', 
  	component: UsersComponent, 
  	children: 
  	[
      { path: ':id/:name', component: UserComponent },
  	] 
  },
];
```

2. 만약 users/ 밑에 children이 있다면 users 템플릿에서 필요한 곳에 

<router-outlet>을 사용해서 랜더링한다.

예시

```
<div class="row">
  <div class="col-xs-12 col-sm-4">
    <div class="list-group">
      <a
        [routerLink]="['/users', user.id, user.name]"
        href="#"
        class="list-group-item"
        *ngFor="let user of users">
        {{ user.name }}
      </a>
    </div>
  </div>
  <div class="col-xs-12 col-sm-4">
    <router-outlet></router-outlet>
  </div>
</div>



```

