
# What is AOT vs JIT?
Angular offers two ways to compile your application:
- Just-in-Time (JIT), which compiles your app in the browser at runtime. This was the default until Angular 8.
- Ahead-of-Time (AOT), which compiles your app and libraries at build time. This is the default since Angular 9.

There are three phases of AOT compilation:
- **Code analysis**: the TypeScript compiler and AOT collector create a representation of the source. The collector does not attempt to interpret the metadata it collects. It represents the metadata as best it can and records errors when it detects a metadata syntax violation.
- **code generation**: In this phase, the compiler's StaticReflector interprets the metadata collected in phase 1, performs additional validation of the metadata, and throws an error if it detects a metadata restriction violation. 
- template type checking (optional): In this optional phase, the Angular template compiler uses the TypeScript compiler to validate the binding expressions in templates. You can enable this phase explicitly by setting the fullTemplateTypeCheck configuration option. 
[More on Angular.io](https://angular.io/guide/aot-compiler#ahead-of-time-aot-compilation)


# What is code folding in Angular?
The compiler can only resolve references to exported symbols in the metadata. Whereas some of the non-exported members are folded while generating the code. i.e Folding is a process in which the collector evaluates an expression during collection and record the result in the .metadata.json instead of the original expression. 
- For example, the collector can evaluate the expression 1 + 2 + 3 + 4 and replace it with the result, 10. This process is called folding. An expression that can be reduced in this manner is foldable.
- Another example, the compiler couldn't refer selector reference because it is not exported,
```javascript
let selector = 'app-root';
@Component({
 selector: selector
})
Will be folded into the inline selector
@Component({
 selector: 'app-root'
})
```
Remember that the compiler can’t fold everything. For example, spread operator on arrays, objects created using new keywords and function calls.
> [More on Angular.io](https://angular.io/guide/aot-compiler#code-folding)


# Angular Lifecycle Hooks:
 * Constructor()
 * OnChange(): Respond when Angular sets or resets data-bound input properties. The method receives a SimpleChanges object of current and previous property values.
 * OnInit(): Initialize the directive or component after Angular first displays the data-bound properties and sets the directive or component's input properties.
 * DoCheck(): Detect and act upon changes that Angular can't or won't detect on its own. Called immediately after ngOnChanges() on every change detection run, and immediately after ngOnInit() on the first run.
	 * AfterContentInit(): Respond after Angular projects external content into the component's view, or into the view that a directive is in. Called once after the first ngDoCheck().
	 * AfterContentChecked(): Respond after Angular checks the content projected into the directive or component. Called after ngAfterContentInit() and every subsequent ngDoCheck().
	 * AfterViewInit(): Respond after Angular initializes the component's views and child views, or the view that contains the directive. Called once after the first ngAfterContentChecked().
	 * AfterViewChecked(): Respond after Angular checks the component's views and child views, or the view that contains the directive. Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().
 * OnDestroy(): Cleanup just before Angular destroys the directive or component. Unsubscribe Observables and detach event handlers to avoid memory leaks. Called immediately before Angular destroys the directive or component.
> [Know more...](https://angular.io/guide/lifecycle-hooks#lifecycle-event-sequence)


# Differentiate between Components and Directives in Angular.
  - **Components** break up the application into smaller parts.
  - **Directives** add behavior to an existing DOM element. 
References:
- https://stackoverflow.com/questions/32680244/directive-vs-component-in-angular
- https://blog.angular-university.io/angular-components-and-directives-for-beginners/


# What is IVY? How it works?
**Ivy is a complete rewrite of Angular’s rendering engine**
Why Ivy?
- 🚀 reach better build times (with a more incremental compilation)
- 🔥 reach better build sizes (with a generated code more compatible with tree-shaking)
- More debugging tools
	- Now you have more tools to debug your applications. You have the new ng object for debugging while running an application in Dev Mode. With this you can now gain access to instances of your components, directives, etc.
- 🔓 unlock new potential features 
	- metaprogramming or higher order components
	- lazy loading of component instead of modules
	- a new change detection system not based on zone.js…
- Improved handling of styles and style merging
	- Handling of styles has been greatly improved in Ivy. Usually what happens is that if there were two competing definitions for a style, then those styles would destructively replace each other. Now they are just merged predictably.
	```javascript
	<div 	[class]="myClasses"
			[class.highlighted]="isHighlighted">
	</div>
	```
- Tree shaking
Tree-shaking refers to the fact that unused codes can be removed. It is handled with the help of static analysis. This does not run any code. The team of Ivy has designed Ivy with Tree-Shaking in mind. Iv can result in breaking down things into smaller, atomic functions. The atomic functions would go on to make your renderer code quite user-friendly.
The tree-shakable features of Angular include:
	- Template syntax
	- Content projection
	- Dependency injection
	- Structural directives
	- Pipes
	- Listeners
	- Lifecycle hooks
	- Queries
- Faster Testing
	- New concepts are added, long-standing performance problems are resolved, and types are improved. 
	- The implementation of TestBed is revamped to make Ivy more efficient. Previously, irrespective of any changes done to the components, TestBed was used to recompiling the entire component while running each test. 
	- However, in Angular Ivy, it recompiles components only when there has been any manual overridden, which avoids recompilation in a majority of tests. It is expected that users can experience a 40 to 50 % increase in speed in their app testing.

- Incremental DOM:
	- Incremental DOM is a library for building up DOM trees and updating them in-place when data changes.
	- JavaScript can be used to extract, iterate over and transform data into calls generating HTMLElements and Text nodes. 
	- It differs from the established virtual DOM approach in that no intermediate tree is created (the existing tree is mutated in-place).
	- This approach significantly reduces memory allocation and GC thrashing for incremental updates to the DOM tree therefore increasing performance significantly in some cases.


# What are directives? What are different types of directives?


# How to reduce bundle size in Angular?
- `ng build --prod --build-optimizer` is a good option for people using less than Angular v5. For newer versions, this is done by default with `ng build --prod`
- Another option is to use module chunking/lazy loading to better split your application into smaller chunks
- Ivy rendering engine comes by default in Angular 9, it offers better bundle sizes
- Make sure your 3rd party deps are tree shakeable. If you're not using Rxjs v6 yet, you should be.
- If all else fails, use a tool like webpack-bundle-analyzer to see what is causing bloat in your modules
- Check if you files are gzipped
There are a few things you can do to help the performance of your application:
- AOT & Tree Shaking (angular-cli does this out of the box). With Angular 9 AOT is by default on prod and dev environment.
- Using Angular Universal A.K.A. server-side rendering (not in cli)
- Web Workers (again, not in cli, but a very requested feature) [More...] (https://github.com/angular/angular-cli/issues/2305)
- Service Workers: [More..](see: https://github.com/angular/angular-cli/issues/4006)
You may not need all of these in a single application, but these are some of the options that are currently present for optimizing Angular performance. I believe/hope Google is aware of the out of the box shortcomings in terms of performance and plans to improve this in the future.


# What is RxJS? What are RxJS subjects, operators?
RxJS is a library for composing asynchronous and callback-based code in a functional, reactive style using Observables. Many APIs such as HttpClient produce and consume RxJS Observables and also uses operators for processing observables. 

References:
- [Subjects](https://www.learnrxjs.io/learn-rxjs/subjects)
- [Operators](https://www.learnrxjs.io/learn-rxjs/operators)


# What is an observable?
Observables provide support for data sharing between publishers and subscribers in an angular application. It is referred to as a better technique for event handling, asynchronous programming, and handling multiple values as compared to techniques like promises.
Observables are not part of the JavaScript language so we need to rely on a popular Observable library called RxJS.

The observables are created using new keyword. Let see the simple example of observable,
```javascript
import { Observable } from 'rxjs';

const observable = new Observable(observer => {
	setTimeout(() => {
		observer.next('Hello from a Observable!');
	}, 2000);
});
```


# Subject vs BehaviourSubject
[Read](https://devsuhas.com/2019/12/09/difference-between-subject-and-behaviour-subject-in-rxjs/)



# What is the difference between promise and observable?
- Observables are Declarative: Computation does not start until subscription; so that they can be run whenever you need the result.
- Promise Execute immediately on creation
- Observables Provide multiple values over time, Promise Provide only one
- Observables Subscribe method is used for error handling which makes centralized and predictable error handling	
- Promise Push errors to the child promises
- Observables Provides chaining and subscription to handle complex applications	
- Promise Uses only .then() clause


# What are the utility functions provided by RxJS?
The RxJS library also provides below utility functions for creating and working with observables.
- Converting existing code for async operations into observables
- Iterating through the values in a stream
- Mapping values to different types
- Filtering streams
- Composing multiple streams

- map() : Used to map values of different data types.
- filter() : Used for filtering streams.
- concat() : Used to concatenate multiple strings.
- merge(): Used to recursively descend into object properties in the source copy, while forming a deep copy of the same.


# What is Data Binding? How many ways it can be done?
- Event Binding:
Enables the application to respond to user input in the target environment
Syntax: 
```javascript
(target)="statement"		
on-target="statement" 
```
- Property Binding:
Enables interpolation of values computed from application data into the HTML
Syntax:
```javascript
{{expression}}
[target]="expression"
bind-target="expression"
```
Type: 		Interpolation, Property, Attribute, Class, Style
- Two-way Binding:
Changes made in the application state gets automatically reflected in the view and vice-versa. The ngModel directive is used for achieving this type of data binding.
Syntax:
```javascript
[(target)]="expression"
bindon-target="expression"
```
Type: Two-way


# What is dependency injection in Angular?
Dependency injection (DI), is an important application design pattern in which a class asks for dependencies from external sources rather than creating them itself. 
Angular comes with its own dependency injection framework for resolving dependencies( services or objects that a class needs to perform its function).
So you can have your services depend on other services throughout your application.


# How is Dependency Hierarchy formed?/ How dependency injection works?


# What is Redux? 
- It is a library which helps us maintain the state of the application. 
- Redux is not required in applications that are simple with the simple data flow, 
- it is used in Single Page Applications that have complex data flow. 
## What Is Flux?
Flux is a data flow architecture created by Facebook back in 2014. 


# What is ng-template, ng-container, ng-content directive?
 - **`<ng-template>`**: As the name suggests the `<ng-template>` is a template element that Angular uses with structural directives (*ngIf, *ngFor, [ngSwitch] and custom directives).
- **`<ng-container>`**: The Angular `<ng-container>` is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM.
- **`<ng-content>`**: You use the `<ng-content></ng-content>` tag as a placeholder for that dynamic content, then when the template is parsed Angular will replace that placeholder tag with your content. Think of it like curly brace interpolation, but on a bigger scale. The technical term for this is "content projection" because you are projecting content from the parent component into the designated child component.
> [Know more...](https://medium.com/@joshblf/wtf-is-ng-content-8382b2a664e1)


# What is ViewEncapsulation and how many ways are there do to do it in Angular?
To put simply, ViewEncapsulation determines whether the styles defined in a particular component will affect the entire application or not. Angular supports 3 types of ViewEncapsulation:
- Emulated: Styles used in other HTML spread to the component
- Native: Styles used in other HTML doesn't spread to the component
- None: Styles defined in a component are visible to all components of the application


# Angular Authentication and Authorization? How to implement Authentication and authorization?
[Using JWT token](https://jasonwatmore.com/post/2019/06/22/angular-8-jwt-authentication-example-tutorial)
- Get and store jwt token
```javascript
@Injectable({ providedIn: 'root' })
export class AuthenticationService {
    private currentUserSubject: BehaviorSubject<User>;
    public currentUser: Observable<User>;

    constructor(private http: HttpClient) {
        this.currentUserSubject = new BehaviorSubject<User>(JSON.parse(localStorage.getItem('currentUser')));
        this.currentUser = this.currentUserSubject.asObservable();
    }

    public get currentUserValue(): User {
        return this.currentUserSubject.value;
    }

    login(username: string, password: string) {
        return this.http.post<any>(`${environment.apiUrl}/users/authenticate`, { username, password })
            .pipe(map(user => {
                // store user details and jwt token in local storage to keep user logged in between page refreshes
                localStorage.setItem('currentUser', JSON.stringify(user));
                this.currentUserSubject.next(user);
                return user;
            }));
    }

    logout() {
        // remove user from local storage to log user out
        localStorage.removeItem('currentUser');
        this.currentUserSubject.next(null);
    }
}
```
	- Send jwt token with every request
```javascript
@Injectable()
export class JwtInterceptor implements HttpInterceptor {
    constructor(private authenticationService: AuthenticationService) { }
    intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        // add authorization header with jwt token if available
        let currentUser = this.authenticationService.currentUserValue;
        if (currentUser && currentUser.token) {
            request = request.clone({
                setHeaders: {
                    Authorization: `Bearer ${currentUser.token}`
                }
            });
        }
        return next.handle(request);
    }
}
```
> [Know more...](https://www.tutorialspoint.com/angular8/angular8_authentication_and_authorization.htm)


# What is an AsyncPipe in Angular? What is the purpose of async pipe?
When an observable or promise returns something, we use a temporary property to hold the content. Later, we bind the same content to the template. 
With the usage of AsyncPipe, the promise or observable can be directly used in a template and a temporary property is not required.
- **Purpose**: The AsyncPipe subscribes to an observable or promise and returns the latest value it has emitted. When a new value is emitted, the pipe marks the component to be checked for changes.


# What are structural directives?


# Accessibility
Accessibility support is one of the important feature of every UI based application. Accessibility is a way of designing the application so that, it is accessible for those having certain disabilities as well. Let us learn the support provided by Angular to develop application with good accessibility.
- While using attribute binding, use attr. prefix for ARIA attributes.
- Use Angular material component for Accessibility. Some of the useful components are LiveAnnouncer and cdkTrapFocu.
- Use native HTML elements wherever possible because native HTML element provides maximum accessibility features. When creating a component, select native html element matching your use case instead of redeveloping the native functionality.
- Use NavigationEnd to track and control the focus of the application as it greatly helps in accessibility.


# What are some points to consider when optimizing an Angular application for performance?

--------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------

# What are web sockets?


# Angular Unit tests:


# Angular versions?


# Angularjs vs Angular


# Compilation:
   * Compiler vs Transpiler vs Interpreter



# How Angular works?
- [Stack overflow](https://stackoverflow.com/questions/50098245/what-exactly-triggers-main-ts-in-angular)
- [Medium blog](https://medium.com/siam-vit/how-an-angular-app-work-behind-the-scenes-angular-flow-dcc4d1df27bd#:~:text=2.-,MAIN.,entry%20point%20of%20the%20application.&text=ts%20file%20calls%20the%20function,builder%20to%20bootstrap%20the%20app.)


# Building blocks of Angular:
 * Components
 * Data Binding
 * Dependency Injection (DI)
 * Directives
 * Metadata
 * Modules
 * Routing
 * Services
 * Template


# Event handling in Angular
> [Know more...](https://angular.io/guide/event-binding)


# How components are lazy loaded in Angular?


# What is viewChild and viewChildren?


# What are web workers?
Web workers enables JavaScript application to run the CPU-intensive tasks in the background so that the application main thread concentrate on the smooth operation of UI. Angular provides support for including Web workers in the application.


# What are components?
- A component(@component) is a directive-with-a-template.
- A class with the @Component() decorator that associates it with a companion template. 
- Together, the component and template define a view. 
- A component is a special type of directive. 
- The @Component() decorator extends the @Directive() decorator with template-oriented features.
	

# What is a module?
NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities. The application is divided into separate modules to separate the functionality of your application.
> [Know more...](https://hackr.io/blog/angular-interview-questions)


# Angular architecture overview


# Why prioritize TypeScript over JavaScript in Angular?
> [Know more...](https://stackoverflow.com/questions/12694530/what-is-typescript-and-why-would-i-use-it-in-place-of-javascript)
> [Know more...](https://dzone.com/articles/what-is-typescript-and-why-use-it#:~:text=TypeScript%20simplifies%20JavaScript%20code%2C%20making%20it%20easier%20to%20read%20and%20debug.&text=TypeScript%20provides%20highly%20productive%20development,huge%20improvement%20over%20plain%20JavaScript.)


# What is the purpose of using package.json in the angular project?
> [package.json](https://nodejs.org/en/knowledge/getting-started/npm/what-is-the-file-package-json/#:~:text=All%20npm%20packages%20contain%20a,as%20handle%20the%20project%27s%20dependencies.&text=The%20package.,-json%20file%20is)


# What does a Subscribe method do in Angular?
It is a method which is subscribed to an observable. Whenever the subscribe method is called, an independent execution of the observable happens.




# Angular design pattern


# What is metadata?
Metadata is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators.
- Class decorators, e.g. @Component and @NgModule
- Property decorators Used for properties inside classes, e.g. @Input and @Output
- Method decorators Used for methods inside classes, e.g. @HostListener
- Parameter decorators Used for parameters inside class constructors, e.g. @Inject


# Decorators,  Annotations


# What is Angular CLI? CLI commands?
Angular CLI(Command Line Interface) is a command line interface to scaffold and build angular apps using nodejs style (commonJs) modules.


# What is the difference between constructor and ngOnInit?
- TypeScript classes has a default method called constructor which is normally used for the initialization purpose. 
- Whereas ngOnInit method is specific to Angular, especially used to define Angular bindings. 
- Even though constructor getting called first, it is preferred to move all of your Angular bindings to ngOnInit method.


# What is a service?
A service is used when a common functionality needs to be provided to various modules. Services allow for greater separation of concerns for your application and better modularity by allowing you to extract common functionality out of components.
- @Injectable decorator converts a plain Typescript class into Angular service:
```javascript
import { Injectable } from '@angular/core'; 
@Injectable({ 
   providedIn: 'root',  // providedIn?: Type<any> | 'root' | 'platform' | 'any' | null
})
export class DebugService { 
   constructor() { } 
}
```
- providedIn: Determines which injectors will provide the injectable, by either associating it with an @NgModule or other InjectorType, or by specifying that this injectable should be provided in one of the following injectors:
	- 'root' : The application-level injector in most apps.
	- 'platform' : A special singleton platform injector shared by all applications on the page.
	- 'any' : Provides a unique instance in each lazy loaded module while all eagerly loaded modules share one instance.
- [Dependency Injection in Action](https://angular.io/guide/dependency-injection-in-action)



# What is the option to choose between inline and external template file?
The choice between inline and separate HTML is a matter of taste, circumstances, and organization policy. But normally we use inline template for small portion of code and external template file for bigger views. By default, the Angular CLI generates components with a template file. But you can override that with the below command, ng generate component hero -it


# What happens if you use script tag inside template?
Angular recognizes the value as unsafe and automatically sanitizes it, which removes the script tag but keeps safe content such as the text content of the script tag. This way it eliminates the risk of script injection attacks. If you still use it then it will be ignored and a warning appears in the browser console.


# What is interpolation?
Interpolation is a special syntax that Angular converts into property binding.


# What are template expressions?
- A template expression produces a value similar to any Javascript expression. 
- Angular executes the expression and assigns it to a property of a binding target; the target might be an HTML element, a component, or a directive. 
- In the property binding, a template expression appears in quotes to the right of the = symbol as in [property]="expression". 
- In interpolation syntax, the template expression is surrounded by double curly braces. 
- The below javascript expressions are prohibited in template expression
	- assignments (=, +=, -=, ...)
	- new
	- chaining expressions with ; or ,
	- increment and decrement operators (++ and --)


# What are template statements?
- A template statement responds to an event raised by a binding target such as an element, component, or directive. 
- The template statements appear in quotes to the right of the = symbol like (event)="statement".
- In the above expression, editProfile is a template statement. The below JavaScript syntax expressions are not allowed.
	- new
	- increment and decrement operators, ++ and --
	- operator assignment, such as += and -=
	- the bitwise operators | and &
	- the template expression operators


# What are pipes?
A pipe takes in data as input and transforms it to a desired output.


# What is a parameterized pipe?
- A pipe can accept any number of optional parameters to fine-tune its output. 
- The parameterized pipe can be created by declaring the pipe name with a colon ( : ) and then the parameter value. 
- If the pipe accepts multiple parameters, separate the values with colons.
>Note: The parameter value can be any valid template expression, such as a string literal or a component property.


# What is a custom pipe?
Apart from built-inn pipes, you can write your own custom pipe with the below key characteristics:
A pipe is a class decorated with pipe metadata @Pipe decorator, which you import from the core Angular library For example,
```javascript
	@Pipe({name: 'myCustomPipe'})
```
The pipe class implements the PipeTransform interface's transform method that accepts an input value followed by optional parameters and returns the transformed value. The structure of pipeTransform would be as below,
```javascript
interface PipeTransform {
	transform(value: any, ...args: any[]): any
}
```
You can create custom reusable pipes for the transformation of existing value. 
For example, let us create a custom pipe for finding file size based on an extension,
```javascript
		import { Pipe, PipeTransform } from '@angular/core';
		
		@Pipe({name: 'customFileSizePipe'})
		export class FileSizePipe implements PipeTransform {
		  transform(size: number, extension: string = 'MB'): string {
			return (size / (1024 * 1024)).toFixed(2) + extension;
		  }
		}
```
Now you can use the above pipe in template expression as below,
	 template: `
		<p>Size: {{288966 | customFileSizePipe: 'GB'}}</p>
	  `


# What is the difference between pure and impure pipe?
- A pure pipe is only called when Angular detects a change in the value or the parameters passed to a pipe. 
- For example, any changes to a primitive input value (String, Number, Boolean, Symbol) or a changed object reference (Date, Array, Function, Object). 
- An impure pipe is called for every change detection cycle no matter whether the value or parameters changes. i.e, An impure pipe is called often, as often as every keystroke or mouse-move.


# What is a bootstrapping module?
Every application has at least one Angular module, the root module that you bootstrap to launch the application is called as bootstrapping module.


# What is HttpClient and its benefits?
Most of the Front-end applications communicate with backend services over HTTP protocol using either XMLHttpRequest interface or the fetch() API. 
- Angular provides a simplified client HTTP API known as HttpClient which is based on top of XMLHttpRequest interface.
- The major advantages of HttpClient can be listed as below,
	- Contains testability features
	- Provides typed request and response objects
	- Intercept request and response
	- Supports Observalbe APIs
	- Supports streamlined error handling
Below are the steps need to be followed for the usage of HttpClient.
	- Import HttpClient into root module
	- Inject the HttpClient into the application
```javascript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
const userProfileUrl: string = 'assets/data/profile.json';
@Injectable()
export class UserProfileService {
  constructor(private http: HttpClient) { }
}
getUserProfile() {
  return this.http.get(this.userProfileUrl);
}
```
- Create a component for subscribing service: Let's create a component called UserProfileComponent(userprofile.component.ts) which inject UserProfileService and invokes the service method,
```javascript
fetchUserProfile() {
  this.userProfileService.getUserProfile()
	.subscribe((data: User) => this.user = {
		id: data['userId'],
		name: data['firstName'],
		city:  data['city']
	});
}
```
Since the above service method returns an Observable which needs to be subscribed in the component.


# How can you read full response?
The response body doesn't may not return full response data because sometimes servers also return special headers or status code which which are important for the application workflow. Inorder to get full response, you should use observe option from HttpClient,
```javascript
getUserResponse(): Observable<HttpResponse<User>> {
  return this.http.get<User>(
	this.userUrl, { observe: 'response' });
}
```
Now HttpClient.get() method returns an Observable of typed HttpResponse rather than just the JSON data.


# How do you perform Error handling?


# What will happen if you do not supply handler for observer?
Normally an observer object can define any combination of next, error and complete notification type handlers. If you don't supply a handler for a notification type, the observer just ignores notifications of that type.


# What are angular elements?
- Angular elements are Angular components packaged as custom elements(a web standard for defining new HTML elements in a framework-agnostic way). 
- Angular Elements hosts an Angular component, providing a bridge between the data and logic defined in the component and standard DOM APIs, thus, providing a way to use Angular components in non-Angular environments.


# What is progressive web app PWA?
Progressive web apps (PWA) are normal web application with few enhancements and behaves like a native application. PWA apps does not depends on network to work. PWA caches the application and renders it from local cache. It regularly checks the live version of the application and then caches the latest version in the background.
## Service worker
At its simplest, a service worker is a script that runs in the web browser and manages caching for an application.

Service workers function as a network proxy. They intercept all outgoing HTTP requests made by the application and can choose how to respond to them. For example, they can query a local cache and deliver a cached response if one is available. Proxying isn't limited to requests made through programmatic APIs, such as fetch; it also includes resources referenced in HTML and even the initial request to index.html. Service worker-based caching is thus completely programmable and doesn't rely on server-specified caching headers.


# What is the browser support of Angular Elements?


# What are custom elements?


# Do I need to bootstrap custom elements?


# Explain how custom elements works internally?


# How to transfer components to custom elements?


# What is component decorators in Angular 4?


# What is compilation in Angular? And what are the types of compilation in Angular?


# What is Template reference variables?



# What are all the types of Directives?


# What are all the uses of a service?


# What is Redux and @ngRx?


# How to prevent security threads in Angular App? What are all the ways we could secure our App?


# How to optimize Angular app?


# What is NgZone service? How Angular is notified about the changes?


# What is Traceur compiler?


# How do you bootstrap the Angular application?


# What is Template input variables?


# What is the expression context in Angular?


# How do components communicate with each other?


# What are the difference between Renderer and ElementRef in Angular?


# What is the difference between @Inject and @Injectable?


# What is Lazy loading?


# What is Shadow DOM in Angular? Does Angular uses Virtual DOM?


# Explain Angular Routing.


# How to link routes in HTML?


# How do we access the Route parameters in Angular?


# How and when do you define a Child route?


# What is the difference between queryParams and routeParams?


# How to restrict or control access from or to a Route? What is Route Guards?


# What is Auxilary Routes?


# What is Redux and @ngRx? What is Action in Redux?


# How do we change the state of our application? What is Reducers?


# What is Change Detection in Angular? How it is improved from Angular 1.x?


# What is ChangeDetectorRef?


# What is NgZone service? How Angular is notified about the changes?


# What are @HostListener and @HostBinding? How can detect events in or set properties on the parent element of a directive?


# What are TemplateRef and ViewContainerRef?


# What is :host-context pseudo-class selector?


# Explain the Template Driven Forms.


# Explain Model Driven Forms or Reactive Forms.
Reactive forms concepts:
- FormControl − Define basic functionality of individual form control
- FormGroup − Used to aggregate the values of collection form control
- FormArray − Used to aggregate the values of form control into an array
- ControlValueAccessor − Acts as an interface between Forms API to HTML DOM elements.


# What's the difference between NgForm, FormGroup, and FormControl?


# How do you add form validation to a form built with FormBuilder?


# How do you add custom validators in Angular?


# What is async validation and how is it done?


# How would you select all the child components' elements?


# What is name of a special function of class which gets called when object is created and it's syntax in Typescript?


# What are the basic rules of Decorators?


# If you do not know the number of arguments to be passed to function in advance, you should use _______ parameter type.


# _____ keyword is used to access class's member variables and functions inside class member function.


# We must import ____________ module to use [(ngModel)].


# Import ____________ module to use reactive form.


# Write an example to define custom event with Boolean argument with code and passing data to parent component.


# Write a syntax to bind custom CSS class (e.g. highlighted) to a <div> tag.


# You can create local HTML reference of HTML tag using variable which starts with character: @ # * &


# You can access HTML local reference alias in component's typescript code using ___________ decorator.


# In template driven form _________ object is created internally whenever we have below code   <form #heroForm='ngForm'>   whereas in reactive form, we have to create this object explicitly.


# Choose correct form control class name which is set to true when value is modified: .ng-valid .ng-invalid .ng-pending .ng-pristine .ng-dirty  .ng-untouched .ng-touched


# If you provide a service in two components providers section of @Component decorator, how many instances of service shall get created?


# When you apply pipe, it changes value of underlying component's member variable as well.


# In routing, below tag is used to show selected route component dynamically


# We need to call below method of RouterModule for providing all routes in AppModule


# What is difference between "declarations", "providers" and "import" in NgModule?


# Why would you use renderer methods instead of using native element methods?


# How would you insert an embedded view from a prepared TemplateRef?


# How to detect a route change in Angular?


# How do you create application to use scss? What changed for Angular?


# Name some security best practices in Angular


# Could I use jQuery with Angular?


# Could you provide some particular examples of using ngZone?


# Why angular uses url segment?


# When to use query parameters versus matrix parameters?


# Write an example of a simple HTML document with some header information and page content.


# In JavaScript, how can the style of an HTML element be changed?


# Write some code for a basic class in TypeScript with a constructor and a method.


# What are Single Page Applications? How do they work in Angular?


# Tell me about a time you received feedback on a task.


# Describe how you would approach solving (some problem) on a high level?


# What are some advantages of using Angular framework for building web applications?


# Write an example usage of ngFor for displaying all items from an array Items in a list with <li>. 


# What modules should you import in Angular to use [(ngModel)] and reactive forms?


# What are HTTP Interceptors?


# How many Change Detectors can there be in the whole application?


# What change detection strategies do you know?


# What is Change Detection, how does Change Detection Mechanism work?


# How do you update the view if your data model is updated outside the Zone?



# Why do we need lazy loading of modules and how is it implemented?


# What are Core and Shared modules for?



# What are some important practices to secure an Angular application?


# Whats the difference between unit testing and end-to-end testing? What are some testing tools you would use for an Angular application?


# Describe a time you fixed a bug/error in an application. How did you approach the problem? What debugging tools did you use? What did you learn from this experience?


# What's the most important thing to look for or check when reviewing another team member's code?


# What tools & practices do you consider necessary for Continuous Integration and Delivery of an Angular application?


# What are es6 modules?

# What is lint?


# What is subscribing?

An Observable instance begins publishing values only when someone subscribes to it. 
So you need to subscribe by calling the subscribe() method of the instance, passing an observer object to receive the notifications. 

Let's take an example of creating and subscribing to a simple observable, with an observer that logs the received message to the console.
Creates an observable sequence of 5 integers, starting from 1
```javascript
const source = range(1, 3);
		
// Create observer object
const myObserver = {
	next: x => console.log('Observer got a next value: ' + x),
	error: err => console.error('Observer got an error: ' + err),
	complete: () => console.log('Observer got a complete notification'),
};

// Execute with the observer object and Prints out each item
myObservable.subscribe(myObserver);
// => Observer got a next value: 1
// => Observer got a next value: 2
// => Observer got a next value: 3
// => Observer got a complete notification
```


# Internationalization (i18n)


# Server Side Rendering
Server side Rendering (SSR) is a modern technique to convert a Single Page Application (SPA) running in the browser into a server based application. Usually, in SPA, the server returns a simple index.html file with the reference to the JavaScript based SPA app. The SPA app take over from there, configure the entire application, process the request and then send the final response.

But in SSR supported application, the server as well do all the necessary configuration and then send the final response to the browser. The browser renders the response and start the SPA app. SPA app takeover from there and further request are diverted to SPA app. The flow of SPA and SSR is as shown in below diagram.


# What is an observer?
Observer is an interface for a consumer of push-based notifications delivered by an Observable. It has below structure,
```javascript
interface Observer<T> {
	closed?: boolean;
	next: (value: T) => void;
	error: (err: any) => void;
	complete: () => void;
}
```
A handler that implements the Observer interface for receiving observable notifications will be passed as a parameter for observable as below,
```javascript
myObservable.subscribe(myObserver);
```
> Note: If you don't supply a handler for a notification type, the observer ignores notifications of that type.


# What is multicasting?
Multi-casting is the practice of broadcasting to a list of multiple subscribers in a single execution. Let's demonstrate the multi-casting feature,

```javascript
var source = Rx.Observable.from([1, 2, 3]);
var subject = new Rx.Subject();
var multicasted = source.multicast(subject);

// These are, under the hood, `subject.subscribe({...})`:
multicasted.subscribe({
	next: (v) => console.log('observerA: ' + v)
});
multicasted.subscribe({
	next: (v) => console.log('observerB: ' + v)
});
// This is, under the hood, `s
```
 
	
# How do you perform error handling in observables?
You can handle errors by specifying an error callback on the observer instead of relying on try/catch which are ineffective in asynchronous environment. 
Example, you can define error callback as below:
```javascript
myObservable.subscribe({
	next(num) { console.log('Next num: ' + num)},
	error(err) { console.log('Received an errror: ' + err)}
});
```


# What is the short hand notation for subscribe method?
The subscribe() method can accept callback function definitions in line, for next, error, and complete handlers is known as short hand notation or Subscribe method with positional arguments. For example, you can define subscribe method as below:
```javascript
myObservable.subscribe(
	x => console.log('Observer got a next value: ' + x),
	err => console.error('Observer got an error: ' + err),
	() => console.log('Observer got a complete notification')
);
```


# What are observable creation functions?
RxJS provides creation functions for the process of creating observables from things such as promises, events, timers and Ajax requests. Let us explain each of them with an example:

Create an observable from a promise
```javascript
import { from } from 'rxjs'; // from function
const data = from(fetch('/api/endpoint')); //Created from Promise
data.subscribe({
	next(response) { console.log(response); },
	error(err) { console.error('Error: ' + err); },
	complete() { console.log('Completed'); }
});
```
Create an observable that creates an AJAX request
```javascript
import { ajax } from 'rxjs/ajax'; // ajax function
const apiData = ajax('/api/data'); // Created from AJAX request
// Subscribe to create the request
apiData.subscribe(res => console.log(res.status, res.response));
```
Create an observable from a counter
```javascript
import { interval } from 'rxjs'; // interval function
const secondsCounter = interval(1000); // Created from Counter value
secondsCounter.subscribe(n =>
console.log(`Counter value: ${n}`));
```
Create an observable from an event
```javascript		
import { fromEvent } from 'rxjs';
const el = document.getElementById('custom-element');
const mouseMoves = fromEvent(el, 'mousemove');
const subscription = mouseMoves.subscribe((e: MouseEvent) => {
	console.log(`Coordnitaes of mouse pointer: ${e.clientX} * ${e.clientY}`);
});
```


# How is SPA (Single Page Application) technology different from the traditional web technology?


# Differentiate between ng-Class and ng-Style.
In ng-Class, loading of CSS class is possible; whereas, in ng-Style we can set the CSS style. 


