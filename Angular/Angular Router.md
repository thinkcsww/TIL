​												Angular Router

------

1. app.module.ts에서 다음과 같이 path와 component를 정해준다.

```
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'servers', component: ServersComponent }
];
```

2. RouterModule을 NgModule에 추가해준다.

```
@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    UsersComponent,
    ServersComponent,
    UserComponent,
    EditServerComponent,
    ServerComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    RouterModule.forRoot(appRoutes)
  ],
  providers: [ServersService],
  bootstrap: [AppComponent]
})
```

3. app.component.html에 <router-outlet></router-outlet>을 넣어주면         <a>태그에 따라서 라우트가 된다. <a>태그 에서는 href가 아닌 routerLink를 사용

```

<ul class="nav nav-tabs">
  <li role="presentation" class="active">
    <a routerLink="/">Home</a>
  </li>
  <li role="presentation">
    <a routerLink="/servers">Servers</a>
  </li>
  <li role="presentation">
    <a routerLink="/users">Users</a>
  </li>
</ul>
<div class="row">
<router-outlet></router-outlet>
</div>


```