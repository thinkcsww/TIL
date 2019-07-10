​					Angular Candeactivate(데이터 수정 후 페이지 이동시 확인)

------

데이터 수정하는 페이지에서 데이터가 하나라도 변한 후에 저장하지 않고 페이지를 이동할 때 데이터가 다 날아가는 것을 막기 위해서 alert를 물어보기 위함.

CanDeactivate를 사용해야 한다.

1. 사용하려고하는 Component와 같은 폴더에 can-deactivate-guard.ts를 만들어준다. 

예시

```
import {Observable} from 'rxjs';
import {ActivatedRouteSnapshot, CanDeactivate, RouterStateSnapshot} from '@angular/router';

export interface CanComponentDeactivate {
  canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean
}

export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {

  canDeactivate(component: CanComponentDeactivate,
                currentRoute: ActivatedRouteSnapshot,
                currentState: RouterStateSnapshot,
                nextState: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
    return component.canDeactivate();
  }
}

```

2. 사용하려는 컴포넌트에 위의 interface를 implements하고 함수안에 원하는 조건에 따라서 boolean을 return하고 페이지를 바꿔도 되면 true를 리턴