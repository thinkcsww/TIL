​											Angular Observable 합치기 

------

두개의 Observable을 하나로 합쳐서 1개처럼 사용하기.

1. Pipe에서 exhaustMap을 사용한다. -> 앞의 Observable에서 필요한 부분을 쓰고 버리고 뒤의 Observable을 subscribe로 return 한다.

```
fetchRecipes() {
    return this.authService.user.pipe(
      take(1),
      exhaustMap(user => {
        console.log(user);
      return this.http
        .get<Recipe[]>('https://ng-pj-c2f10.firebaseio.com/recipes.json?auth=' + user.token)
    }),
    map(recipes => {
        return recipes.map(recipe => {
          return {...recipe, ingredients: recipe.ingredients ? recipe.ingredients : []};
        });
      }),
      tap(recipes => {
        this.recipesService.setRecipes(recipes);
      }));
  }
```

