​										Angular 404 route 설정하기

------

1. app.module.ts의 appRoutes의 맨 아래에 path: '**'로 연결하고 redirectTo 404 컴포넌트로 redirect한다.

```
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
      { path: ':id/:name', component: UserComponent },
  ] },

  { path: 'servers', component: ServersComponent, children: [
      { path: ':id', component: ServerComponent },
      { path: ':id/edit', component: EditServerComponent },
  ] },
  { path: 'not-found', component: PageNotFoundComponent},
  { path: '**', redirectTo: '/not-found'},

];

```

2. 아래처럼 하면 에러가 없어진다. 근데 무슨 에러지? 모든 url은 ''로 시작하기 때문에 path를 아래처럼 하면 에러가 생긴다는 말인듯?

```
{ path: '', redirectTo: '/somewhere-else', pathMatch: 'full' }
```

