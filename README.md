Angular Tutorial
=================

This repository will walk step by step to teach you the basics of angular.
Each step is commited in its own commit so you can perform diff/pull request
To see what was changed between each steps.

### Kickstart

The following code was executed to create this angular project
* Install all the requirements

    `npm install -g @angular/cli`

* Create the project skelton

    `ng new angularTutorial`  
    `cd angularTutorial`

* Development server

    Run `ng serve` for a dev server.   
    Navigate to `http://localhost:4200/`  
    The app will automatically reload if you change any of the source files.
    
### Step 01 - Basics
Lets navigate through the diffrent project fiels to get idea what is going on

- Make sure `ng serve` is running and open the browser on `http://localhost:4200/`  
- Change the application title inside the `app.component.ts`
- Change the `app/component.html` to display the title 

### Step 02 - Create manual components
We are going to create new component   

- Create new folder named `serevr` under the `app` folder. 
- Inside the folder create the following new files
   
   - `server.component.css`
   - `server.component.html`
   - `server.component.ts` 

- Define the component in the `server.component.ts`   
  View the code to see whats is required.
- Register the component inside `app.module.ts`   

### Step 03 - Create components using the CLI
Instead of creating manual components we will create one using the CLI commands.  

- In your terminal type `ng generate component servers`   
or short way: `ng g c servers`
- Update the html code to the `servers.component.html`

### Step 04 - Adding bootstrap CSS
- install bootstrap `npm i bootstrap`
- Add the bootstrap css path to the `.angular-cli.json`
- Add html code to verify that the css is loaded

### Step 05 - Data Binding
Data binding allow us to add dynamic content to the application.    
There are several forms of Binding. Lets start with the simple one

- Edit the `ServerComponent` inside the `server.component.ts` and add the variables and the method as appear in the source code
- Edit the template `server.component.html` and add the binding code to display the content

### Step 06 - Property Binding
At this step we update property using timer and the changes will be reflacted in the code. We will add and update button state.
- Edit `servers.component.ts` and add the required code
- The syntax for property binding is `[<html propery>]=<angular property>`
- To boind attribute like dataset use the `[attr.<attribute name>]` => `[attr.data-allow]="allowNewServer"`

### Step 07 - Event Binding
- The synatx for adding an event bunding is using `(<event name>)="<event handler>"`
- Edit `servers.component.ts` and add the required variables and methods
- Update the component html and add the required code. In this step we demonstrated the prevoius bindings as well.

### Step 08 - 2 way binding
In the preovoius step we have demostarted 2 way binding. Lets dive into it now.
- 2Way bindign allow us to display iitial values of the property for example
- The syntax is combination of `[] && ()` => `[(ngModel)]`
- Add the import `FormsModule` inside the `app.module.ts` (import declation & inside the imports array).
  **!NOte: `FormsModule` should be in `imports` not in `declarations`**
- Declare the `ngModel` inside our `servers.component.html`

### Step 09 - Directives
- Directives are html extentions (DOM) which are being created from templates (usually not always).
- Directives are usually attributes
- The syntax is `*` for example : `*ngIf=...`
    
    #### ngIf (Structural directive)
    - `ngIf` is used to conditionaly display content.
    - The simple way is to use it as attribute
    - We can also us it with `local reference` for `if else` syntax

    #### ngStyle / ngClass
    - `ngStyle` is used to conditionaly add style to an element.
    - `ngClass` is used to conditionaly add css class to an element.
        - Add the required css code
        - Replace the `[attr.data-allow]="allowNewServer"` with ngClass code from the source

### Step 10 - Multiple components
Create multiple components and add communication between them
- For this step we will need to get familier with `ngFor` Directive, so read about it before starting this step.
- You can simply checkout this step and copy the content. This steps will be used as placeholder for the content. If you wish to do it your self follow the steps below.
- Create the first component without testing specs `ng g c cockpit --spec false`
- Create the second component without testing specs `ng g c server-element --spec false`
- Copy the initial html code from the `cockpit.component.html` to your componenet
- Copy the content of the `server-element.component.html` into your component
- Copy the content of the `app.component.ts`
- Copy the content of the `app.component.html`

#### At this point the project should be broken and you will see the following message
`Property 'serverElements' does not exist on type 'CockpitComponent'.`
- To fix it for now we will comment out the code so we can continue.

### Step 11 - Binding custom properties
- Add the required code inside the `server-element.component.ts`. This code define our custom element
- Inside the `app.component.ts` define the `serverElements`, again copy it from the initial code.
- Add the `[element]` property to the `app.component.html`.  
  At this point we should see error (*in the browser console*) since the property can be accessed only from within `server-element` component and we are adding it to the app component
- In order to "expose" it to parent component we need to add `decorator` **`@Input()`** to the element.  
  Dont forget to add the required import as well

### Step 12 - Binding custom events
- In this step we want to notify the parent component that inner component was updated
- Update the `app.component.ts` with the event handlers code
- Update the `app.component.html` to support the new event we created
- Add the 2 custom event data in `cockpit.component.ts`. Make sure to expose them with `EventEmitter` & `@Output()`  
  Dont forget to add the required import as well
- Inside `cockpit.component.ts` fire (emit) the events

# Directives
***
### 13 - Attriute directives
* First lets start with attribute directives
* Create a new folder `src/app/directives/highlight`
* Create the directive file `src/app/directives/highlight/highlight.directive.ts`
  ```js
  import { Directive, ElementRef, OnInit } from '@angular/core';

  @Directive({
    selector: '[appBasicHighlight]'
  })

  export class BasicHighlightDirective implements OnInit {
    constructor(private elementRef: ElementRef) {
    }

    ngOnInit() {
      this.elementRef.nativeElement.style.backgroundColor = 'green';
    }
  }

  ```
* Register the directive in the app module 
* Add the attribute directive to the app template
  ```html
  <div class="container">
    ...
    <p appHighlight>This is our appHighlight directive</p>
    ...
  </div> 
  ```

### step14 - Directive Render
* Lets create a new direcive and this time with the CLI command
  ```
  $ ng g d directives/text-highlight --spec false

  # We should now see the following output
  create src/app/directives/text-highlight.directive.ts
  update src/app/app.module.ts
  ```
* Add the required code to the `directives/text-highlight.directive.ts`
* Add the directive to the template and verify that its working

### step15 - Directive Events
* In this step we will interact with the directive
* In order to do it we need to add `HostListener` - which will be used for our mouse events
* Add the `HostListener` to the directive from prevoius step
  ```js 
    @HostListener( <enent_name>) <function_name> (<Event data>) 
  ```
### step16 - Directive Properies (HostBinding)
* In this atep we will be chnaging one of the nodes property like style, class etc.
* First of all add `HostBinding` to the directive
* Add the property we wish to bind to 
  ```js
  # In our case we wish to bind the style.backgroundColor property 
  @HostBinding('style.backgroundColor') bgColor: string;
  ```
* Update the code in the `HostListener`
  ```js
    @HostListener('mouseleave') mouseleave(event: Event) {
      this.bgColor = 'transparent';
      this.color = 'black';
    }
  ```
### step17 - Directive Properies (readProperty)
* Instead of having the colors hard code we wish to read them from the element
* Fisrt add the `Input` decorator
  ```js
  // Add the input fields
  @Input() defaultBgColor: string;
  @Input() hoverBgColor: string;

  // Initialize values
   
  ```
* Add the required attribute colors in `ngOninit`
  ```js
    ngOnInit() {

    // Set the defaults ...
    this.bgColor = this.defaultBgColor;
    this.color = this.defaultColor;
    
    ...

  ```
### step18 - Structural Directives
* In the prevoius steps we used attribute directives, now we will add structural directives
* Lets create a new directive using the CLI which wil be opposite to the ng-if
  ```
    ng g d unless --spec false
  ```
* We need to get the condition as input from the element so we need to add the `@Input`
* Since we also need to listen to changes we will add the `set` keywork to the `@Input`
  **The name of the property must be the same as the directive name**
  ```js
  @Input() set appUnless(condition: boolean) {}
  ```
* Add the contractor properties (template & view)
  ```js
  constructor(
    private templateRef: TemplateRef<any>,
    private vcRef: ViewContainerRef
  ) { }
  ```
* Now update the unless `@Input()` logic
  ```js
  @Input() set appUnless(condition: boolean) {
    if (!condition) {
      this.vcRef.createEmbeddedView(this.templateRef);
    } else {
      this.vcRef.clear();
    }
  }
  ```  
* Add the required code to the `app.component.html`
  ```html
      <div *appUnless="true">This is the content when *appUnless="true" </div>
      <div *appUnless="false">This is the content when *appUnless="false" </div>
  ```
* Practice: 
  * Add property to the app component to control if the unless is visible or not