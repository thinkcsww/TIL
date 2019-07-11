​							Angular Data Binding을 통한 Component 간의 통신

1. @Input

   1. 다른곳에서 사용할 Component의 맴버 변수에 @Input Notation을 붙인다.

   2. 사용하는 곳에서 [input 맴버 변수] = "[값]"을 넣어준다.

   3. 사용할 Component 

   4. ```
      ...
      export class RecipeItemComponent implements OnInit {
        @Input() recipe: Recipe;
      }
      ```

   4. 사용하는 Component 

   ```
   <app-recipe-item
         *ngFor="let recipeEl of recipes"
         [recipe]="recipeEl"></app-recipe-item>
   ```

   

2. @Output

   1. 보낼 맴버변수에 @Output을 붙여주고 new EventEmitter<Generic>()로 초기화 해준다. 
   2. 받는 곳에서 (output 맴버변수)="함수 or 바로 처리"
   3. 보내는 Component

   ```
   export class RecipeItemComponent implements OnInit {
     @Output() recipeSelected = new EventEmitter<void>();
   }
   ```

   4. 받는 Component

   ```
   <app-recipe-item
     *ngFor="let recipeEl of recipes"
     (recipeSelected)="onRecipeSelected(recipeEl)"></app-recipe-item>
     
     onRecipeSelected(recipe: Recipe) {
     	this.recipeWasSelected.emit(recipe);
     }
   ```