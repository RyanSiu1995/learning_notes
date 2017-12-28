* High Level Architecture

  * Module \(NgModules\)

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

* Data Binding
  * 



