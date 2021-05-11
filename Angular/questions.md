# Angular Questions

## Angular versions?

## Compilation:
   ### Compiler vs Transpiler vs Interpreter
   ### JIT vs AOT

##
	
----------------------------------------------------------------------------------------
Reference: https://hackr.io/blog/angular-interview-questions

1. What is ng-template, ng-container, ng-content directive?
	<ng-template>: As the name suggests the <ng-template> is a template element that Angular uses with structural directives (*ngIf, *ngFor, [ngSwitch] and custom directives).
	<ng-container>: The Angular <ng-container> is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM.
	<ng-content>: 	You use the <ng-content></ng-content> tag as a placeholder for that dynamic content, 
					then when the template is parsed Angular will replace that placeholder tag with your content. 
					Think of it like curly brace interpolation, but on a bigger scale. 
					The technical term for this is â€œcontent projection" because you are projecting content 
					from the parent component into the designated child component.
					Reference: https://medium.com/@joshblf/wtf-is-ng-content-8382b2a664e1

2. Enumerate some salient features of Angular 7.
	Splitting in @angular/core. This is done in order to reduce the size of the same. 
	Typically, not each and every module is required by an Angular developer. 
	Angular 7 each split of the @angular/core will have no more than 418 modules.
	drag-and-drop and virtual scrolling
	a new and enhanced version of the ng-compiler.
	
	
4. What are the building blocks of Angular?
	Components
	Data Binding
	Dependency Injection (DI)
	Directives
	Metadata
	Modules
	Routing
	Services
	Template
	
5. Can you give us an overview of Angular architecture?
	Architecture diagram in official documentation.
	
6. What is Angular Material?
	It is a UI component library.
	
7. What is AOT (Ahead-Of-Time) Compilation?
	In Angular, it means that the code you write for your application is compiled at build time before the application is run in a browser. 
	More details needed!
	
8. What is Data Binding? How many ways it can be done?
	a. Event Binding:
		Enables the application to respond to user input in the target environment
		Syntax:		(target)="statement"		on-target="statement"
	b. Property Binding:
		Enables interpolation of values computed from application data into the HTML
		Syntax:		{{expression}}		[target]="expression"		bind-target="expression"
		Type: 		Interpolation, Property, Attribute, Class, Style
	c. Two-way Binding:
		Changes made in the application state gets automatically reflected in the view and vice-versa. The ngModel directive is used for achieving this type of data binding.
		Syntax:		 [(target)]="expression"		bindon-target="expression"
		Type: 		Two-way
		
9. What is ViewEncapsulation and how many ways are there do to do it in Angular?
	To put simply, ViewEncapsulation determines whether the styles defined in a particular component will affect the entire application or not. 
	Angular supports 3 types of ViewEncapsulation:
	Emulated â€“ Styles used in other HTML spread to the component
	Native â€“ Styles used in other HTML doesnâ€™t spread to the component
	None â€“ Styles defined in a component are visible to all components of the application
	==== Needs modification as per official docs ====
	
10. Why prioritize TypeScript over JavaScript in Angular?
	==== Needs modification ====
	
11. Explain Angular Authentication and Authorization.
	==== Needs modification ====
----------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------
Reference: https://www.greycampus.com/blog/programming/top-30-interview-questions-and-answers-on-angular-5

1. What is Angular and Why Angular?
	Angular is a platform and framework for building client applications
	==== Needs modification ====
	
2. Differentiate between Components and Directives in Angular.
	Components break up the application into smaller parts
	Directives add behavior to an existing DOM element. 
	
3. How to handle Events in Angular?
	==== Needs modification ====
	
4. What is the sequence of Angular Lifecycle Hooks?
	Constructor()
	OnChange()
	OnInit()
	DoCheck()
		AfterContentInit()
		AfterContentChecked()
		AfterViewInit()
		AfterViewChecked()
	OnDestroy()
	
5. What is the purpose of using package.json in the angular project?
	To manage the dependencies of the project. 
	If we are using typescript in the angular project then we can mention the typescript package and version of typescript in package.json.
	==== Needs modification ====
	
6. How is SPA (Single Page Application) technology different from the traditional web technology? 
	In traditional web technology, the client requests for a web page (HTML/JSP/asp) and the server sends the resource (or HTML page), 
	and the client again requests for another page and the server responds with another resource. 
	The problem here is a lot of time is consumed in the requesting/responding or due to a lot of reloading. 
	Whereas, in the SPA technology, we maintain only one page (index.HTML) even though the URL keeps on changing. 
	==== Needs modification ====
	
7. What does a Subscribe method do in Angular?
	It is a method which is subscribed to an observable. 
	Whenever the subscribe method is called, an independent execution of the observable happens.
	
8. What is an AsyncPipe in Angular?
	When an observable or promise returns something, we use a temporary property to hold the content. 
	Later, we bind the same content to the template. 
	With the usage of AsyncPipe, the promise or observable can be directly used in a template and a temporary property is not required. 
	==== Needs modification ====
	
9. What is Redux? 
	It is a library which helps us maintain the state of the application. 
	Redux is not required in applications that are simple with the simple data flow, 
	it is used in Single Page Applications that have complex data flow. 
	
11. Differentiate between ng-Class and ng-Style.
	In ng-Class, loading of CSS class is possible; whereas, in ng-Style we can set the CSS style. 
----------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------
Reference: https://github.com/sudheerj/angular-interview-questions

1	What is the difference between AngularJS and Angular?
	==== Needs modification ====
	
2	What are components?
	A component(@component) is a directive-with-a-template.
	A class with the @Component() decorator that associates it with a companion template. 
	Together, the component and template define a view. 
	A component is a special type of directive. 
	The @Component() decorator extends the @Directive() decorator with template-oriented features.
	
3	What is a module?
	NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities. 
	The application is divided into separate modules to separate the functionality of your application.

13	What is metadata?
	Metadata is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators.
	a. Class decorators, e.g. @Component and @NgModule
	b. Property decorators Used for properties inside classes, e.g. @Input and @Output
	c. Method decorators Used for methods inside classes, e.g. @HostListener
	d. Parameter decorators Used for parameters inside class constructors, e.g. @Inject
	
14	What is Angular CLI?
	Angular CLI(Command Line Interface) is a command line interface to scaffold and build angular apps using nodejs style (commonJs) modules.

15	What is the difference between constructor and ngOnInit?
	TypeScript classes has a default method called constructor which is normally used for the initialization purpose. 
	Whereas ngOnInit method is specific to Angular, especially used to define Angular bindings. 
	Even though constructor getting called first, it is preferred to move all of your Angular bindings to ngOnInit method.
	
16	What is a service?
	A service is used when a common functionality needs to be provided to various modules. 
	Services allow for greater separation of concerns for your application and 
	better modularity by allowing you to extract common functionality out of components.

17	What is dependency injection in Angular?
	Dependency injection (DI), is an important application design pattern 
	in which a class asks for dependencies from external sources rather than creating them itself. 
	Angular comes with its own dependency injection framework for resolving dependencies
	( services or objects that a class needs to perform its function).
	So you can have your services depend on other services throughout your application.
	
18	How is Dependency Hierarchy formed?

19	What is the purpose of async pipe?
	The AsyncPipe subscribes to an observable or promise and returns the latest value it has emitted. 
	When a new value is emitted, the pipe marks the component to be checked for changes.

20	What is the option to choose between inline and external template file?
	The choice between inline and separate HTML is a matter of taste, circumstances, and organization policy. 
	But normally we use inline template for small portion of code and external template file for bigger views. 
	By default, the Angular CLI generates components with a template file. But you can override that with the below command,
		ng generate component hero -it

23	What happens if you use script tag inside template?
	Angular recognizes the value as unsafe and automatically sanitizes it, 
	which removes the <script> tag but keeps safe content such as the text content of the <script> tag. 
	This way it eliminates the risk of script injection attacks. 
	If you still use it then it will be ignored and a warning appears in the browser console. 

24	What is interpolation?
	Interpolation is a special syntax that Angular converts into property binding. 

25	What are template expressions?
	A template expression produces a value similar to any Javascript expression. 
	Angular executes the expression and assigns it to a property of a binding target; the target might be an HTML element, a component, or a directive. 
	In the property binding, a template expression appears in quotes to the right of the = symbol as in [property]="expression". 
	In interpolation syntax, the template expression is surrounded by double curly braces. 
	The below javascript expressions are prohibited in template expression
		a. assignments (=, +=, -=, ...)
		b. new
		c. chaining expressions with ; or ,
		d. increment and decrement operators (++ and --)
	
26	What are template statements?
	A template statement responds to an event raised by a binding target such as an element, component, or directive. 
	The template statements appear in quotes to the right of the = symbol like (event)="statement".
	In the above expression, editProfile is a template statement. The below JavaScript syntax expressions are not allowed.
		a. new
		b. increment and decrement operators, ++ and --
		c. operator assignment, such as += and -=
		d. the bitwise operators | and &
		e. the template expression operators

27	How do you categorize data binding types?
	a. Event Binding:
		Enables the application to respond to user input in the target environment
		Syntax:		(target)="statement"		on-target="statement"
	b. Property Binding:
		Enables interpolation of values computed from application data into the HTML
		Syntax:		{{expression}}		[target]="expression"		bind-target="expression"
		Type: 		Interpolation, Property, Attribute, Class, Style
	c. Two-way Binding:
		Changes made in the application state gets automatically reflected in the view and vice-versa. The ngModel directive is used for achieving this type of data binding.
		Syntax:		 [(target)]="expression"		bindon-target="expression"
		Type: 		Two-way

28	What are pipes?
	A pipe takes in data as input and transforms it to a desired output.
	
29	What is a parameterized pipe?
	A pipe can accept any number of optional parameters to fine-tune its output. 
	The parameterized pipe can be created by declaring the pipe name with a colon ( : ) and then the parameter value. 
	If the pipe accepts multiple parameters, separate the values with colons.
	Note: The parameter value can be any valid template expression, such as a string literal or a component property.

31	What is a custom pipe?
	Apart from built-inn pipes, you can write your own custom pipe with the below key characteristics:
	A pipe is a class decorated with pipe metadata @Pipe decorator, which you import from the core Angular library For example,
		@Pipe({name: 'myCustomPipe'})
	The pipe class implements the PipeTransform interface's transform method that accepts an input value followed by 
	optional parameters and returns the transformed value. The structure of pipeTransform would be as below,
		interface PipeTransform {
		  transform(value: any, ...args: any[]): any
		}
		
	You can create custom reusable pipes for the transformation of existing value. 
	For example, let us create a custom pipe for finding file size based on an extension,

		import { Pipe, PipeTransform } from '@angular/core';
		
		@Pipe({name: 'customFileSizePipe'})
		export class FileSizePipe implements PipeTransform {
		  transform(size: number, extension: string = 'MB'): string {
			return (size / (1024 * 1024)).toFixed(2) + extension;
		  }
		}
	Now you can use the above pipe in template expression as below,

	 template: `
		<p>Size: {{288966 | customFileSizePipe: 'GB'}}</p>
	  `
	  
33	What is the difference between pure and impure pipe?
	A pure pipe is only called when Angular detects a change in the value or the parameters passed to a pipe. 
	For example, any changes to a primitive input value (String, Number, Boolean, Symbol) or a changed object reference (Date, Array, Function, Object). 
	An impure pipe is called for every change detection cycle no matter whether the value or parameters changes. 
	i.e, An impure pipe is called often, as often as every keystroke or mouse-move.

34	What is a bootstrapping module?
	Every application has at least one Angular module, the root module that you bootstrap to launch the application is called as bootstrapping module.

35	What are observables?
	Observables are declarative which provide support for passing messages between publishers and subscribers in your application. 
	They are mainly used for event handling, asynchronous programming, and handling multiple values. 
	In this case, you define a function for publishing values, but it is not executed until a consumer subscribes to it. 
	The subscribed consumer then receives notifications until the function completes, or until they unsubscribe.

36	What is HttpClient and its benefits?
	Most of the Front-end applications communicate with backend services over HTTP protocol using either XMLHttpRequest interface or the fetch() API. 
	Angular provides a simplified client HTTP API known as HttpClient which is based on top of XMLHttpRequest interface.
	The major advantages of HttpClient can be listed as below,
		- Contains testability features
		- Provides typed request and response objects
		- Intercept request and response
		- Supports Observalbe APIs
		- Supports streamlined error handling
	Below are the steps need to be followed for the usage of HttpClient.
		- Import HttpClient into root module
		- Inject the HttpClient into the application
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
		- Create a component for subscribing service: Let's create a component called UserProfileComponent(userprofile.component.ts) which inject UserProfileService and invokes the service method,
				fetchUserProfile() {
				  this.userProfileService.getUserProfile()
					.subscribe((data: User) => this.user = {
						id: data['userId'],
						name: data['firstName'],
						city:  data['city']
					});
				}
	Since the above service method returns an Observable which needs to be subscribed in the component.
		
38	How can you read full response?
	The response body doesn't may not return full response data because sometimes servers also return special headers or status code which 
	which are important for the application workflow. Inorder to get full response, you should use observe option from HttpClient,
		getUserResponse(): Observable<HttpResponse<User>> {
		  return this.http.get<User>(
			this.userUrl, { observe: 'response' });
		}
	Now HttpClient.get() method returns an Observable of typed HttpResponse rather than just the JSON data.

39	How do you perform Error handling?
	==== Need modification ====
	
40	What is RxJS?
	RxJS is a library for composing asynchronous and callback-based code in a functional, reactive style using Observables. 
	Many APIs such as HttpClient produce and consume RxJS Observables and also uses operators for processing observables. 
	
41	What is subscribing?

	An Observable instance begins publishing values only when someone subscribes to it. 
	So you need to subscribe by calling the subscribe() method of the instance, passing an observer object to receive the notifications. 
	Let's take an example of creating and subscribing to a simple observable, with an observer that logs the received message to the console.

	Creates an observable sequence of 5 integers, starting from 1
		const source = range(1, 5);

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
		// => Observer got a next value: 4
		// => Observer got a next value: 5
		// => Observer got a complete notification
		
42	What is an observable?
	An Observable is a unique Object similar to a Promise that can help manage async code. 
	Observables are not part of the JavaScript language so we need to rely on a popular Observable library called RxJS. 
	The observables are created using new keyword. Let see the simple example of observable,

		import { Observable } from 'rxjs';

		const observable = new Observable(observer => {
		  setTimeout(() => {
			observer.next('Hello from a Observable!');
		  }, 2000);
		});
	
43	What is an observer?
	Observer is an interface for a consumer of push-based notifications delivered by an Observable. It has below structure,
		interface Observer<T> {
		  closed?: boolean;
		  next: (value: T) => void;
		  error: (err: any) => void;
		  complete: () => void;
		}
	A handler that implements the Observer interface for receiving observable notifications will be passed as a parameter for observable as below,
		myObservable.subscribe(myObserver);
	Note: If you don't supply a handler for a notification type, the observer ignores notifications of that type.
	
44	What is the difference between promise and observable?
	Observables are Declarative: Computation does not start until subscription so that they can be run whenever you need the result.
	Promise Execute immediately on creation
	Observables Provide multiple values over time
	Promise Provide only one
	Observables Subscribe method is used for error handling which makes centralized and predictable error handling	
	Promise Push errors to the child promises
	Observables Provides chaining and subscription to handle complex applications	
	Promise Uses only .then() clause
	
45	What is multicasting?
	Multi-casting is the practice of broadcasting to a list of multiple subscribers in a single execution. 
	Let's demonstrate the multi-casting feature,

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
	
46	How do you perform error handling in observables?
	You can handle errors by specifying an error callback on the observer instead of relying on try/catch which are ineffective in asynchronous environment. 
	For example, you can define error callback as below,

	myObservable.subscribe({
	  next(num) { console.log('Next num: ' + num)},
	  error(err) { console.log('Received an errror: ' + err)}
	});

47	What is the short hand notation for subscribe method?
	The subscribe() method can accept callback function definitions in line, for next, error, 
	and complete handlers is known as short hand notation or Subscribe method with positional arguments. 
	For example, you can define subscribe method as below,

	myObservable.subscribe(
	  x => console.log('Observer got a next value: ' + x),
	  err => console.error('Observer got an error: ' + err),
	  () => console.log('Observer got a complete notification')
	);
	
48	What are the utility functions provided by RxJS?
	The RxJS library also provides below utility functions for creating and working with observables.
		- Converting existing code for async operations into observables
		- Iterating through the values in a stream
		- Mapping values to different types
		- Filtering streams
		- Composing multiple streams
	
49	What are observable creation functions?
	RxJS provides creation functions for the process of creating observables from things such as promises, events, timers and Ajax requests. 
	Let us explain each of them with an example,

	Create an observable from a promise
		import { from } from 'rxjs'; // from function
		const data = from(fetch('/api/endpoint')); //Created from Promise
		data.subscribe({
		 next(response) { console.log(response); },
		 error(err) { console.error('Error: ' + err); },
		 complete() { console.log('Completed'); }
		});
	Create an observable that creates an AJAX request
		import { ajax } from 'rxjs/ajax'; // ajax function
		const apiData = ajax('/api/data'); // Created from AJAX request
		// Subscribe to create the request
		apiData.subscribe(res => console.log(res.status, res.response));
	Create an observable from a counter
		import { interval } from 'rxjs'; // interval function
		const secondsCounter = interval(1000); // Created from Counter value
		secondsCounter.subscribe(n =>
		  console.log(`Counter value: ${n}`));
	Create an observable from an event
		import { fromEvent } from 'rxjs';
		const el = document.getElementById('custom-element');
		const mouseMoves = fromEvent(el, 'mousemove');
		const subscription = mouseMoves.subscribe((e: MouseEvent) => {
		  console.log(`Coordnitaes of mouse pointer: ${e.clientX} * ${e.clientY}`);
		});
	
50	What will happen if you do not supply handler for observer?
	Normally an observer object can define any combination of next, error and complete notification type handlers. 
	If you don't supply a handler for a notification type, the observer just ignores notifications of that type.
	
51	What are angular elements?
	Angular elements are Angular components packaged as custom elements(a web standard for defining new HTML elements in a framework-agnostic way). 
	Angular Elements hosts an Angular component, providing a bridge between the data and logic defined in the component and standard DOM APIs, 
	thus, providing a way to use Angular components in non-Angular environments.

52	What is the browser support of Angular Elements?
	
	
53	What are custom elements?
54	Do I need to bootstrap custom elements?
55	Explain how custom elements works internally?
56	How to transfer components to custom elements?
----------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------
Reference: https://medium.com/@vigowebs/frequently-asked-angular-interview-questions-and-answers-d996be87cc7c

1.  What is Angular 4 and how it differs from Angular 1.x?
2.  What is component decorators in Angular 4?
3.  What is compilation in Angular 4? And what are the types of compilation in Angular 4?
4.  What is @NgModule?
5.  What are all the metadata properties of NgModule? And what are they used for?
6.  What is Template reference variables?
7.  What are structural directives?
8.  What is Directive in Angular 4? How it differs from Components?
9.  What are all the types of Directives?
10. What are all the uses of a service?
11. What is Pure and Impure Pipes?
12. What is Redux and @ngRx?
13. How to prevent security threads in Angular App? What are all the ways we could secure our App?
14. How to optimize Angular app?
15. What is NgZone service? How Angular is notified about the changes?
16. What is Traceur compiler?
----------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------
Reference: http://blog.vigowebs.com/post/2018/angular5-interview-questions/

1.  What is Angular 4 and how it differs from Angular 1.x?
2.  What is Component in Angular 4? How do you declare them?
3.  What is component decorators in Angular 4?
4.  What is compilation in Angular 4? And what are the types of compilation in Angular 4?
5.  What is @NgModule? What are all the metadata properties of NgModule? And what are they used for?
6.  How do you bootstrap the Angular 4 application?
7.  What is Template reference variables?
8.  What is Template input variables?
9.  What are structural directives?
10. What does asterisk (*) syntax means in the structural directives?
11. What is <ng-template>?
12. What is Component lifecycle?
13. What is the expression context in Angular 4?
14. What are all the binding categories in Angular?
15. Explain the different types of bindings available in Angular?
16. What is Directive in Angular 4? How it differs from Components?
17. What are all the types of Directives?
18. How do components communicate with each other?
19. What are the difference between Renderer and ElementRef in Angular 4?
20. What is an Angular 4 Services?
21. What are all the uses of a service?
22. What is the difference between @Inject and @Injectable?
23. What is Pipe in Angular? What is Pure and Impure Pipes?
24. What is Lazy loading?
25. What is View Encapsulation?
26. What is Shadow DOM in Angular 4? Does Angular uses Virtual DOM?
27. Explain Angular Routing.
28. How to link routes in HTML?
29. How do we access the Route parameters in Angular?
30. How and when do you define a Child route?
31. What is the difference between queryParams and routeParams?
32. How to restrict or control access from or to a Route? What is Route Guards?
33. What is Auxilary Routes?
34. What is Redux and @ngRx? What is Action in Redux?
35. How do we change the state of our application? What is Reducers?
36. What is Side-effects? How to handle them?
37. How to prevent security threads in Angular App? What are all the ways we could secure our App?
38. How to optimize Angular app?
39. What is Change Detection in Angular? How it is improved from Angular 1.x?
40. What is ChangeDetectorRef?
41. What is NgZone service? How Angular is notified about the changes?
42. What are @HostListener and @HostBinding? How can detect events in or set properties on the parent element of a directive?
43. What are TemplateRef and ViewContainerRef?
44. Explain AOT in Angular?
45. What is Traceur compiler?
46. What is the difference between constructor and ngOnInit?
47. What is :host-context pseudo-class selector?
48. How Two-way data binding works in Angular 2? Is it same like Anglar 1.x? Explain the Two-way data binding in Angular?
49. What is the difference between Template driven forms and Model driven forms (or Reactive forms)?
50. Explain the Template Driven Forms.
51. Explain Model Driven Forms or Reactive Forms.
52. What's the difference between NgForm, FormGroup, and FormControl?
53. How do you add form validation to a form built with FormBuilder?
54. How do you add custom validators in Angular?
55. What is async validation and how is it done?
56. How would you select all the child components' elements?
57. What is Observables in Angular?
----------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------
Reference: https://medium.com/@balramchavan/angular-2-4-5-and-6-interview-questions-set-1-a632b9dec579

1.  What is name of a special function of class which gets called when object is created and itâ€™s syntax in Typescript?
2.  What are the basic rules of Decorators?
3.  If you do not know the number of arguments to be passed to function in advance, you should use _______ parameter type.
4.  _____ keyword is used to access classâ€™s member variables and functions inside class member function.
5.  In Angular, you can pass data from parent component to child component using
6.  In Angular, you can pass data from child component to parent component using
7.  Write a syntax for ngFor with <li> example.
8.  We must import ____________ module to use [(ngModel)].
9.  Import ____________ module to use reactive form.
10. Write an example to define custom event with Boolean argument with code and passing data to parent component.
11. Write a syntax to bind custom CSS class (e.g. highlighted) to a <div> tag.
12. You can create local HTML reference of HTML tag using variable which starts with character: @ # * &
13. You can access HTML local reference alias in componentâ€™s typescript code using ___________ decorator.
14. In template driven form _________ object is created internally whenever we have below code   <form #heroForm=â€ngFormâ€?>   whereas in reactive form, we have to create this object explicitly.
15. Choose correct form control class name which is set to true when value is modified: .ng-valid .ng-invalid .ng-pending .ng-pristine .ng-dirty  .ng-untouched .ng-touched
16. If you provide a service in two componentsâ€? â€œprovidersâ€? section of @Component decorator, how many instances of service shall get created?
17. When you apply â€˜pipeâ€?, it changes value of underlying componentâ€™s member variable as well.
18. In routing, below tag is used to show selected route component dynamically
19. We need to call below method of RouterModule for providing all routes in AppModule
----------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------
Reference: https://www.fullstack.cafe/blog/21-expert-angular-interview-questions

1.  What is difference between "declarations", "providers" and "import" in NgModule?
2.  What is AOT?
3.  Explain the difference between "Constructor" and "ngOnInit"
4.  What's new in Angular 6 and why shall we upgrade to it?
5.  Why would you use renderer methods instead of using native element methods?
6.  What is Zone in Angular?
7.  Why would you use lazy loading modules in Angular app?
8.  What are the lifecycle hooks for components and directives?
9.  How would you insert an embedded view from a prepared TemplateRef?
10. How to detect a route change in Angular?
11. What does a just-in-time (JIT) compiler do (in general)?
12. How do you create application to use scss? What changed for Angular 6?
13. What is ngUpgrage?
14. What is Reactive programming and how does it relate to Angular?
15. Name some security best practices in Angular
16. Could I use jQuery with Angular?
17. What is the Angular equivalent to an AngularJS "$watch"?
18. Just-in-Time (JiT) vs Ahead-of-Time (AoT) compilation. Explain the difference.
19. Do you know how you can run angularJS and angular side by side?
20. Could you provide some particular examples of using ngZone?
21. Why angular uses url segment?
22. When to use query parameters versus matrix parameters?
----------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------
Reference: https://www.devteam.space/hiring-interview-tips/35-angular-interview-questions-and-answers/

1. Write an example of a simple HTML document with some header information and page content.
2. Briefly explain the CSS box model. Write some code snippets to describe show what you mean.
3. In JavaScript, how can the style of an HTML element be changed?
4. Write some code for a basic class in TypeScript with a constructor and a method.
5. What are Single Page Applications? How do they work in Angular?
6. Whatâ€˜s the basic syntax of a Decorator in Angular?
7. What is [(ngModel)] used for?
8. What are the basic parts of an Angular application?
9. Tell me about a time you received feedback on a task.
10. Describe how you would approach solving (some problem) on a high level?
11. What are some advantages of using Angular framework for building web applications?
12. What function is called when an object is created in TypeScript? What is itâ€˜s basic syntax in TypeScript code?
13. In Angular, how can you interact between Parent and Child components? 
14. Write an example usage of ngFor for displaying all items from an array â€™Itemsâ€? in a list with <li>. 
15. What is the sequence of Angular Lifecycle Hooks?
16. If you provide a service in two componentsâ€? â€œprovidersâ€? section of @Component decorator, how many instances of service shall get created?
17. What is the main difference between constructor and ngOnInit?
18. What modules should you import in Angular to use [(ngModel)] and reactive forms?
19. How similar is AngularJS to Angular 2?
20. What were some features introduced in the different versions of Angular (2, 4, 5 and 6)?
21. What is Transpiling in Angular?
22. What is AOT Compilation?
23. What are HTTP Interceptors?
24. How many Change Detectors can there be in the whole application?
25. What change detection strategies do you know?
26. What is Change Detection, how does Change Detection Mechanism work?
27. How do you update the view if your data model is updated outside the â€˜Zoneâ€??
28. Why do we need lazy loading of modules and how is it implemented?
29. What are Core and Shared modules for?
30. What are some points to consider when optimizing an Angular 6 application for performance?
31. What are some important practices to secure an Angular application?
32. Whatâ€˜s the difference between unit testing and end-to-end testing? What are some testing tools you would use for an Angular application?
33. Describe a time you fixed a bug/error in an application. How did you approach the problem? What debugging tools did you use? What did you learn from this experience?
34. Whatâ€™s the most important thing to look for or check when reviewing another team memberâ€™s code?
35. What tools & practices do you consider necessary for Continuous Integration and Delivery of an Angular application?
----------------------------------------------------------------------------------------


Reference: hacks.mozilla.org/2015/08/es6-in-depth-modules

1.  What are es6 modules?
2.  What's the difference between compilers and transpilers?
3.  What are decorators?
4.  
5.  


-------------------------------------------------------------------------------------------

1. Which of the Angular life cycle component execution happens when a data-bound input value updates?
		ngOnChanges()
