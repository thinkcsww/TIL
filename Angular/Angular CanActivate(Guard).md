​																	Angular CanActivate(Guard)

------

UrlTree는 말그대로 url이다. 조건에 맞지 않을 때 특정 url로 redirect 할 수 있다. 자동으로 subscribe 해준다.

True를 리턴하면 접근가능, 아니면 불가

1. 일정 조건이 만족되지 않을 때 접근을 막고 redirect 해주는 서비스

2. <이름.guard.ts>의 파일을 만들고 CanActivate를 implements한다.

```
@Injectable({providedIn: 'root'})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}
  canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
    return this.authService.user.pipe(
      take(1),
      map(user => {
        const isAuth = !!user;
        if (isAuth) {
          return true;
        }
        return this.router.createUrlTree(['/auth']);
      })
    );
  }
}
```

3. App-routing-module.ts에서 필요한 route에 canActivate를 추가해준다.

```
const appRoutes: Routes = [
  { path: 'recipes', component: RecipesComponent,
    canActivate: [AuthGuard],
    children: [
    { path: '', component: RecipeStartComponent },
    { path: 'new', component: RecipeEditComponent },
    { path: ':id', component: RecipeDetailComponent, resolve: [RecipesResolverService] },
    { path: ':id/edit', component: RecipeEditComponent },
  ] },
];
```

