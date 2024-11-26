# Boot Process of Angular Apps   

1. to compile the application use following command.  
```bash 
$ ng serve
```

2. "main.ts" file is the file everuthing start your angular application.  
>src/main.ts  
```ts 
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}
// here "bootstrap" is the application that we inform it, use the "AppModule" . 
// every module can have multiple modules.  
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

3. inside "AppModule" there are one component by default named "AppComponent", there we can define multiple components and modules in future here.       
>src/app/app.module.ts  
```ts 
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent // starting component  
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

4. if we change something on "main.ts" file it can be effect in "test.ts" file.  
>src/test.ts  
```ts 
// This file is required by karma.conf.js and loads recursively all the .spec and framework files

import 'zone.js/testing';
import { getTestBed } from '@angular/core/testing';
import {
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting
} from '@angular/platform-browser-dynamic/testing';

declare const require: {
  context(path: string, deep?: boolean, filter?: RegExp): {
    <T>(id: string): T;
    keys(): string[];
  };
};

// First, initialize the Angular testing environment.
getTestBed().initTestEnvironment(
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting(),
);

// Then we find all the tests.
const context = require.context('./', true, /\.spec\.ts$/);
// And load the modules.
context.keys().forEach(context);
```

5. in "index.html" file you can see only basic html file with "<app-root></app-root>" directive. And it say to angular that angular output add it to inside "app-root" directive.     
>src/index.html   
```ts 
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>HelloWorld</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
</body>
</html>
```

6. in the "app.component.ts" file you can see "app-root" as selector and it say that whatever the output should go to "app-root" in the html file.   
>src/app/app.component.ts  
```ts 
import { Component } from '@angular/core;';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'hello-world';
}
```

in above "app.module.ts" file show "AppComponent" as "bootstrap" that 


7. Rendering and Dynamic Code Injection.  
when you run angular application and r-click>view-source than see very basic html page and when you r-click>inspect than you can see in the "app-root" element the angular generated elements. So we can understand that angular will add it code generation dynamically and inject in to html "app-root" element in runtime.   

delete everything except "router-outlet" in the "app.component.html" file and add something like to test in the browser. 
```html 
<h1>{{title}}</h1>
<router-outlet></router-outlet>
```

8. show how to transfile angular application.   
when you do following command it will transfile you Typescript code in to Javascript code.   
```bash 
$ ng serve  
```

and it will generate following list of es6 Javascript files. Any code update will regenerate following files.   
```ts 
1. main.js – Contains the main application logic.
2. polyfills.js – Provides support for Angular's features in different browsers.
3. vendor.js – Contains third-party libraries and dependencies.
4. styles.js – Includes global stylesheets.
5. runtime.js – Handles the application's runtime environment.
```  

