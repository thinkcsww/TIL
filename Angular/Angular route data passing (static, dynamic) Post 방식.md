​									Angular route data passing (static, dynamic) Post 방식?

1. Static

   1. route에서 data attribute를 사용해서 넘긴다.

   ```
   const appRoutes: Routes = [
   	{ path: 'not-found', component: ErrorPageComponent, data: { message: 'Page not found!' }},
   ]
   ```

   

   2. component에서 route<ActivatedRoute>를 사용해서 받는다. (ActivatedRoute를 inject해줘야됨)

   ```
   ...
   constructor(
       private route: ActivatedRoute,
     ) { }
    // 방법 1 - 1회성? 
   this.errorMessage = this.route.snapshot.data['message'];
   // 방법 2 - reactive method
   this.route.data.subscribe(
   (data: Data) => {
   this.errorMessage = data['message'];
   }
   )
   ```



2. Dynamic 

   1. 쓰려고 하는 컴포넌트 폴더에 Resolver를 만든다.  <name>-resolver.service.ts

   ```
   import {ActivatedRouteSnapshot, Resolve, RouterStateSnapshot} from '@angular/router';
   import {Observable} from 'rxjs';
   import {ServersService} from '../servers.service';
   import {Injectable} from '@angular/core';
   
   interface Server {
     id: number;
     name: string;
     status: string;
   }
   
   @Injectable()
   export class ServerResolverService implements Resolve<Server> {
   
     constructor(private serversService: ServersService) {}
   
     resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Server> | Promise<Server> | Server {
       return this.serversService.getServer(+route.params['id']);
     }
   }
   
   ```

   

   2. route에서 resolve attribute를 사용해서 resolver 객체를 넘긴다. 

   ```
   const appRoutes: Routes = [
   	{ path: ':id', component: ServerComponent, resolve: { server: ServerResolverService }}
   ]
   ```

   

   3. 컴포넌트에서 사용한다. 

   ```
   ...
   constructor(
       private route: ActivatedRoute,
     ) { }
    
    ngOnInit() {
       this.route.data
         .subscribe(
           (data: Data) => {
             this.server = data['server'];
           }
         );
     }
     
   ```

   



