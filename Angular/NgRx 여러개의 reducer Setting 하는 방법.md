​																	NgRx 여러개의 reducer Setting 하는 방법

------

1. 여러개의 reducer를 구현한다.
2. App 루트에 store 폴더와 app.reducer.ts 파일을 생성한다.
3. 여러개의 reducer를 import 하고 state와 reducer를 합친다. - 

2개가 있을 때 예제

```
import * as fromShoppingList from '../shopping-list/store/shopping-list.reducer';
import * as fromAuth from '../auth/store/auth.reducer';
import { ActionReducerMap } from '@ngrx/store';

export interface AppState {
  shoppingList: fromShoppingList.State;
  auth: fromAuth.State;
}

export const appReducer: ActionReducerMap<AppState> = {
  shoppingList: fromShoppingList.shoppingListReducer,
  auth: fromAuth.authReducer,
};

```

4. app.modules.ts에 StoreModule에 설정해준다.

```
@NgModule({
  declarations: [AppComponent, HeaderComponent],
  imports: [
    BrowserModule,
    HttpClientModule,
    AppRoutingModule,
    StoreModule.forRoot(fromApp.appReducer),
    SharedModule,
    CoreModule
  ],
  bootstrap: [AppComponent],
  // providers: [LoggingService]
})
```



끝.