* High Level Architecture

  * Module \(NgModules\)

    * @NgModule decorator

      * declare - components, directives and pipes

      * imports - other NgModules 

      * provide - services

      * bootstrap - root components

      * exports - 

    * Bundle native application & extend the application

    * Lazy loading the modules

      * Each modules can be loaded into Angular as long as the route touch

    * ```typescript
      // Eager import
      import { ModuleWithProviders } from '@angular/core';
      import { Routes, RouterModule } from '@angular/router';
      import { moduleA, routeArrA } from './moduleA';
      import { moduleB, routeArrB } from './moduleB';

      const normalRoutes: Routes = [
        { path: '', redirectTo: 'A', pathMatch: 'full' },
        { path: 'A', children: routeArrA }, 
        { path: 'B', children: routeArrB }
      ];

      const routing: ModuleWithProviders = RouterModule.forRoot(routes);

      @NgModules{
          imports: [
              moduleA,
              moduleB,
              normalRoutes
          ]
      }

      // Lazy Load
      const lazyRoutes: Routes = [
        { path: '', redirectTo: 'eager', pathMatch: 'full' },
        // loadChildren: 'pathToModule#className'
        // No need to import the routeArr and modules separately
        // It will automatically inject into the AppModule
        { path: 'A', loadChildren: 'moduleA#moduleA' },
        { path: 'B', loadChildren: 'moduleB#moduleB' }
      ];

      @NgModules{
          imports: [
              lazyRoutes
          ]
      }
      ```

      forRoot and forChild

      * These functions are used for shared modules with providers in both eager and lazy module. These define what providers should be exported.

      * forRoot registers the providers globally

      * forChild registers the providers locally. It can override the global provider.

      * ```typescript
        // With forChild and forRoot
        @NgModule({
            providers: [AService]
        })
        export class A {
            forRoot() {
                return {
                    ngModule: A,
                    providers: [AService]
                }
            }
            forChild() {
                return {
                    ngModule: A,
                    providers: [BService]
                }
            }
        }
        // Without forChild and forRoot
        @NgModule({
            providers: [AService]
        })
        class A {}
        export const moduleWithProvidersForRoot = {
            ngModule: A,
            providers: [AService]
        };
        export const moduleWithProvidersForChild = {
            ngModule: A,
            providers: [BService]
        };
        ```

        Reference: 

        1. [https://stackoverflow.com/questions/40498081/routermodule-forrootroutes-vs-routermodule-forchildroutes/44680396](https://stackoverflow.com/questions/40498081/routermodule-forrootroutes-vs-routermodule-forchildroutes/44680396)

        2. [https://blog.angularindepth.com/avoiding-common-confusions-with-modules-in-angular-ada070e6891f](https://blog.angularindepth.com/avoiding-common-confusions-with-modules-in-angular-ada070e6891f)

    * 

* Data Binding

  * 



