​																		NgRx 기본

------

각각의 State는 Immutable 하기 때문에 항상 deep clone해서 새로 만들어진 state를 변경해서 사용한다.

npm install —save @ngrx/store

1. Reducer - initial state를 가지고 새로운 state를 store에 return하는 곳, store의 state를 변경할 수 있는 곳, 
2. Action - 어떤 일을 할지 reducer에게 알려주는 action?
3. Dispatch - 컴포넌트에서 action을 부르는 일?
4. Store - State를 저장하는 모든 것을 포괄하는 개념





1. 먼저 Action을 만든다.

1. action의 이름을 변수로 선언해준다. -> 에러 방지

```
export const ADD_INGREDIENT = 'ADD_INGREDIENT';
export const ADD_INGREDIENTS = 'ADD_INGREDIENTS';
```

2. Action을 선언한다. 

```
export class AddIngredient implements Action {
  readonly type = ADD_INGREDIENT;

  constructor(public payload: Ingredient) {}
}

export class AddIngredients implements Action {
  readonly type = ADD_INGREDIENTS;

  constructor(public payload: Ingredient[]) {}
}

export type ShoppingListActions = AddIngredient | AddIngredients;
```



2. Reducer를 먼저 만든다. 
   1. initialState를 만든다.

```
// model화
export interface State {
  ingredients: Ingredient[];
  editedIngredient: Ingredient;
  editedIngredientIndex: number;
}

// app.module.ts에 쓰기 위해서 
export interface AppState {
  shoppingList: State;
}

const initialState: State = {
  ingredients: [
    new Ingredient('Apples', 5),
    new Ingredient('Tomatoes', 10),
  ],
  editedIngredient: null,
  editedIngredientIndex: -1,
};

```

2. reducer를 만든다.

```
	export function shoppingListReducer(
  state: State = initialState,
  action: ShoppingListActions.ShoppingListActions) {
  switch (action.type) {
    case ShoppingListActions.ADD_INGREDIENT:
      return {
        ...state,
        ingredients: [...state.ingredients, action.payload]
      };
    case ShoppingListActions.ADD_INGREDIENTS:
      return {
        ...state,
        ingredients: [...state.ingredients, ...action.payload]
      };
    case ShoppingListActions.UPDATE_INGREDIENT:
      const ingredient = state.ingredients[state.editedIngredientIndex];
      const updatedIngredient = {
        ...ingredient,
        ...action.payload
      };

      const updatedIngredients = [ ...state.ingredients ];
      updatedIngredients[state.editedIngredientIndex] = updatedIngredient;

      return {
        ...state,
        ingredients: updatedIngredients,
        editedIngredientIndex: -1,
        editedIngredient: null
      };
    case ShoppingListActions.DELETE_INGREDIENT:
      return {
        ...state,
        ingredients: state.ingredients.filter((_, index) => {
          return index !== state.editedIngredientIndex;
        }),
        editedIngredientIndex: -1,
        editedIngredient: null
      };
    case ShoppingListActions.START_EDIT:
      return {
        ...state,
        editedIngredientIndex: action.payload,
        editedIngredient: { ...state.ingredients[action.payload] }
      };
    case ShoppingListActions.STOP_EDIT:
      return {
        ...state,
        editedIngredientIndex: -1,
        editedIngredient: null
      };
    default:
      return state;
  }
}
```

3. app.module.ts에 Reducer를 추가한다.

```
@NgModule({
  declarations: [AppComponent, HeaderComponent],
  imports: [
  	...
    StoreModule.forRoot({shoppingList: shoppingListReducer}),
    ...
  ],
  bootstrap: [AppComponent],
  // providers: [LoggingService]
})
```



4. Dispatch - Component에서 store로 필요한 일을 한다.

1. 단순 데이터 가져오기 - Store에서 가져오는 State는 모두 Observable이다.

```
import * as fromShoppingList from ....
....
ingredients: Observable<{ ingredients: Ingredient[] }>;

...
constructor(
		...
    private store: Store<fromShoppingList.AppState>
  ) {}
 
 ngOnInit() {
 // this.ingredients는 observable이다 
    this.ingredients = this.store.select('shoppingList');
    
    Or 
    
    this.store.select('shoppingList').subscribe((stateData) => {
    	// Do Something
    })
  }

```

1. ```
   // 템플릿에서 observable이기 때문에 pipe를 사용해서 list를 불러올 수 있다.
   <a
           *ngFor="let ingredient of (ingredients | async).ingredients; let i = index"
         >
   ```

   2. 데이터 변경하기 - dispatch만 하면 action에서 일을 처리 ..

   ```
   ...
   import * as ShoppingListActions from '../store/shopping-list.actions';
   
    constructor(private store: Store<{ shoppingList: { ingredients: Ingredient[]} }>) { }
   ...
   
   // 필요한 곳에서 dispatch한다.
   const value = form.value;
   const newIngredient = new Ingredient(value.name, value.amount);
   this.store.dispatch(new ShoppingListActions.AddIngredient(newIngredient));
   ...
   ```

   