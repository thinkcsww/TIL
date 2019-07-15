​																				Angular Resolver		

------

Resolver는 컴포넌트가 Route로 이동전에 필요한 데이터를 받아놓는 일을 한다. 

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
const appRoutes: Routes = [
		...
    { path: ':id', component: RecipeDetailComponent, resolve: [RecipesResolverService] }
    ...
];
```

