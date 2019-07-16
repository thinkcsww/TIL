​																				Angular Resolver		

------

Resolver는 컴포넌트가 Route로 이동전에 필요한 데이터를 받아놓는 일을 한다. 자동으로 Observable을 subscribe한다

1. recipes.service.ts

```
import {Injectable} from "@angular/core";
import {ActivatedRouteSnapshot, Resolve, RouterStateSnapshot} from "@angular/router";
import {Recipe} from "./recipe.model";
import {DataStorageService} from "../shared/data-storage.service";
import {RecipeService} from "./recipe.service";

@Injectable({providedIn: 'root'})
export class RecipesResolverService implements Resolve<Recipe[]> {
  constructor(private dataStorageService: DataStorageService, private recipesService: RecipeService) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot) {
    const recipes = this.recipesService.getRecipes();

    // 시작인 경우 or reload 한 경우
    if (recipes.length === 0 ) {
      return this.dataStorageService.fetchRecipes();
    } else {
      return recipes;
    }
  }
}

```

2. app-routing.modules.ts

```
경우 1
const appRoutes: Routes = [
		...
    { path: ':id', component: RecipeDetailComponent, resolve: [RecipesResolverService] }
    ...
];

------------------------------------------------------------------------
경우 2
{ path: ':id', component: ServerComponent, resolve: { server: ServerResolverService } },
```

3. 경우 1일 때는 service에 저장을 한다던지 하기 때문에 굳이 경우 2처럼 subscribe 필요가 없는듯..

```
@Injectable({providedIn: 'root'})
export class RecipesResolverService implements Resolve<Recipe[]> {
  constructor(private dataStorageService: DataStorageService, private recipesService: RecipeService) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Recipe[]> | Promise<Recipe[]> | Recipe[] {
    const recipes = this.recipesService.getRecipes();

    // 시작인 경우 or reload 한 경우
    if (recipes.length === 0 ) {
      return this.dataStorageService.fetchRecipes();
    }
  }
}
```



4. 경우 2일 때는 컴포넌트에서 다음과 같이 데이터를 받아 사용하면 된다. 

```
 ngOnInit() {
    // resolver에서 데이터를 받는 Logic
    this.route.data
      .subscribe(
        (data: Data) => {
          this.server = data['server'];
        }
      );
  }
```

r