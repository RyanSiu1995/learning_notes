* High Level Architecture
  * Module \(NgModules\)
    * Bundle native application & extend the application

    * Lazy loading the modules

      * Each modules can be loaded into Angular as long as the route touch

      * ```typescript
        // Normal import
        import { ModuleWithProviders } from '@angular/core';
        import { Routes, RouterModule } from '@angular/router';
        import { moduleA, routeA } from './moduleA';
        import { moduleB, routeB } from './moduleB';

        const routes: Routes = [
          { path: '', redirectTo: 'A', pathMatch: 'full' },
          // Assume set the route.forChild in moduleA and moduleB
          // This ways
          { path: 'A', children: routeA }, 
          { path: 'B', children: routeB }
        ];

        const routing: ModuleWithProviders = RouterModule.forRoot(routes);

        @NgModules{
            imports: [
                moduleA,
                moduleB,
                routing
            ]
        }

        // Lazy Load
        const routes: Routes = [
          { path: '', redirectTo: 'eager', pathMatch: 'full' },
          { path: 'eager', component: EagerComponent },
          { path: 'lazy', loadChildren: 'lazy/lazy.module#LazyModule' }
        ];

        export routes
        ```
* Data Binding
  * 



