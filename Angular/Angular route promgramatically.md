​										Angular route promgramatically

------

1. 자동 router와 마찬가지로 app.module.ts에 path와 component를 정해준다.

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

3. 버튼을 만든다. 

```
<button (click)="onLoadServers()"></button>
```

4. Router를 constructor로 inject하고 해당 함수를 정의해준다.

```
import { Component, OnInit } from '@angular/core';
import {Router} from '@angular/router';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor(private router: Router) { }

  onLoadServers() {
    this.router.navigate(['servers']);
  }

}

```

