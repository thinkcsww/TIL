​																		Angular Module 과 lazy loading

------

Module은 크게 3종류로 나뉜다.

1. Feature Module - 음식 어플이라면 Recipe, Shopping-list 등의 굵직한 내용
2. Shared Module - Alert, loader, Common 등의 공유되는 내용, export 필수
   (Component가 자신이 아닌 다른 Module에서 쓰이기 때문) 
3. Core Module - 각종 service들, interceptor 등등 



모듈화를 하게되면 route도 바꿔야하는데 기존에는 app.module에 다 모아서 RouterModule.forRoot()를 사용했다면

```
const appRoutes: Routes = [
  { path: '', redirectTo: '/recipes', pathMatch: 'full' },
];

@NgModule({
  imports: [RouterModule.forRoot(appRoutes)],
  exports: [RouterModule]
})
```

각각 모듈의 route에서는 RouterModule.forChild()를 사용하면 된다.



------

Lazy loading을 사용하게 되면 route를 다르게 설정하게 되고 app.module에서 import도 다르게 한다. 

LazyLoading은 해당 route로 갔을 때 해당 모듈을 로딩하는 방법이기 때문에 app.module에서 모듈을 import하지 않고

다음과 같이 한다. 

CanActivate는 loading 후 체크한다. 꼭 필요하다면 Canload를 쓰라네.

그러나 CanActivate와 Preloading을 같이 쓰는것으로도 충분하다고 한다.

1. 이것을 보면 Recipe나 Auth, Shopping list가 import 안되어 있다.

```
@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule,
    SharedModule,
    CoreModule
  ],
  bootstrap: [AppComponent],

})
export class AppModule {
}

```

2.  이것을 보면 loadChildren에 모듈들이 들어가 있다.

```
const appRoutes: Routes = [
  { path: '', redirectTo: '/recipes', pathMatch: 'full' },
  { path: 'recipes', loadChildren: './recipes/recipes.module#RecipesModule' },
  { path: 'shopping-list', loadChildren: './shopping-list/shopping-list.module#ShoppingListModule'},
  { path: 'auth', loadChildren: './auth/auth.module#AuthModule'}
];

@NgModule({
  imports: [RouterModule.forRoot(appRoutes)],
  exports: [RouterModule]
})
```



이렇게 하면 완성!!!



Preloading을 사용하는 방법, Canactivate와 같이 쓰면 좋다.

```
@NgModule({
  imports: [RouterModule.forRoot(appRoutes, { preloadingStrategy: PreloadAllModules })],
  exports: [RouterModule]
})
```



Preloading은 어떤 route만 preloading 할지 정할 수 있는데 방법은 찾아봐야하는 군요.