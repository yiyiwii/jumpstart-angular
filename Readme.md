# Angular Jumpstart

> Learning note of Udemy course: [Angular - the complete guide](https://www.udemy.com/course/the-complete-guide-to-angular-2)

## Section 2: The Basics

### Component

It is actually a class. In the code, it is a sub-folder inside `app` folder. It includes (`.ts`, `.html`, `css`) files. 

Creat new component (**Assignment 1, practicing components**):
1. manually creat it.
2. use angular CLI: `ng generate component CompnentName` 

Component Decorator
```
@Component({
    selector: 
    template:
    styleUrls:
})
```

#### Data Binding

Data binding is a process that creates a connection between the application's UI and the data. It can be one-way (the change in the data model affects the view) or two-way (a change from the view also change the model).

| Type                                                  | Syntax                                                                | Category                                |
|-------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------|
| Interpolation, Property,<br>  Attribute, Class, Style | ``` {{expression}} [target]="expression" bind-target="expression" ``` | One-way from data source to view target |
| Event                                                 | ``` (target)="statement" on-target="statement" ```                    | One-way from view target to data source |
| Two-way                                               | ``` [(target)]="expression" bindon-target="expression" ```            | Two-way                                 |

Angular supports:

* Interpolation: it uses `{{value}}` inside a UI element. The text between the braces (a template expression) is the name of a component property. 

* Property binding: used to bind values to the DOM properties of the HTML elements. Are evaluated on every browser event and any changes made to the objects in the event are applied to the properties. 

* Event binding 

* Two-way binding


#### Property Binding vs String Interpolation

```
<button class="btn tn-primary" [disabled]="!allowNewComponent">Add Server</button>
<p [innerText]="allowNewServer"></p>

src="{{ recipe.imagePath }}"
[src]="recipe.imagePath"
```

#### Event Binding

```
<button 
    class="btn tn-primary" 
    [disabled]="!allowNewComponent" 
    (click)="onCreateServer()">
    Add Server
</button>
```

#### Two-way binding (property binding + event binding)

Need to enable the `ngModel` directive, which is done by adding the `FormsModel` to the `imports[]` array in the AppModule.

To Learn: [Source] (https://blog.thoughtram.io/angular/2016/10/13/two-way-data-binding-in-angular-2.html)


### Directives 

Directives are instructions in the DOM (document object model). They are used to specify behavior on that DOM element.

```
<p appTurnGreen>Receives a green background!</p>
@Directive({
    selector: '[appTurnGreen]
})
export class TurnGreenDirective {
    ...
}
```

#### `ngIf`: output data conditionally 
```
<button class="btn btn-primary" (click)="showSecret = !showSecret">Display Details</button>
<p *ngIf="showSecret">Secret Password = tuna</p>
```

#### `ngStyle`: style elements dynamically

#### `ngClass`: apply CSS classes dynamically

#### `ngFor`: output Lists

#### Assignment 2 (section 2): Databinding

```
<input type="text" class="form-control" [(ngModel)]="username">
<p>{{ username }}</p>
<button
  class="btn btn-primary"
  [disabled]="username === ''"
  (click)="username = ''">Reset User</button>
```

#### Assignment 3 (section 2): Practicing Directives

```
<!-- app.component.html-->
      <button class="btn btn-primary" (click)="onToggleDetails()">Display Details</button>
      <p *ngIf="showSecret">Secret Password = tuna</p>
      <div
        *ngFor="let logItem of log; let i = index"
        [ngStyle]="{backgroundColor: i >= 4 ? 'blue' : 'transparent'}"
        [ngClass]="{'white-text': i >= 4}">
        {{ logItem }}
      </div>
```

```
// app.component.ts
export class AppComponent {
  showSecret = false;
  log = [];

  onToggleDetails() {
    this.showSecret = !this.showSecret;
    this.log.push(new Date());
  }

}
```

## Section 3: Course Project 1 - The Basics

Generage new component, `recipes`, by CLI:
```
ng g c recipes --skipTests true
```

#### Add a model 

```
export class Ingredient {
  public name: string;
  public amount: number;

  constructor(name: string, amout: number) {
    this.name = name;
    this.amount = amout;
  }
}

// equal to 

export class Ingredient {
    constructor(public name: string, public amount: number) {}
}
```

## Section 5: Components & Databinding Deep Dive

* HTML Elements: native properties & events
* Directives: custom properties & events
* Component: custom properties & events

#### View Encapsulation

To learn: shadown DOM

```
@Component({
  ...,
  encapsulation: ViewEncapsulation.Emulated // None, Native, ShadowDom
})
```

#### use local references in templates

We can declare a reference variable by using hash symble (`#`). Then we can access the variable anythere only inside the template (`.html`).

```
<input type="text" #firstNameInput>
<button (click)="show(lastNameInput)">Show</button>
```

#### `ViewChild` decorator

It a property decorator which configures a view query. With `@ViewChild`, we can inject any component or directive (or HTML element) present on the template of a given component onto the component itself.

#### Getting access to the template & DOM with `@ViewChild`
```
export class ServerElementComponent {
  ...
    @ViewChild('heading', {static: true}) header: ElementRef;
}
```

#### `ng-content` to project content into Component

#### Component Lifecycle

* `ngOnChanges`: called after a bound input property changes
* `ngOnInit`: called once the component is initialized
* `ngDoCheck`: called during every change detection run
* `ngAfterContentInit`: called after content (ng-content) has been projected into view
* `ngAfterContentChecked`: called every time the projected content has been checked
* `ngAfterViewInit`: called after the component's view (and child views) has been initialized
* `ngAfterViewChecked`: called every time the view (and the child views) have been checked
* `ngOnDestroy`: called once the component is about to be destroyed

#### Getting access to `ng-content` with `@ContentChild()` 

#### Assignment 4 (section 5): practicing property & event binding and view encapsulation


## Section 6: Course Project 2 - Components & Databing

* Adding navigation with event binding and `ngIf`

* Passing recipe data with property binding

* Passing data with event and property binding (combined)

* Allowing the user to add ingredients to the shopping list

## Section 7: Directives Deep Dive
> Directives: Custom attributes that enhance HTML syntax and are used to attach behaviors to specific elements on the page.

#### `ngFor` and `ngIf` recap

The `ngIf` directive is used to insert/remove/show an element according to the true/false condition. The `ngFor` is used to display each item in a list.

```
// in .html file
<div *ngIf="onlyOdd">
  <li
    class="list-group-item"
    [ngClass]="{odd: odd % 2 !== 0}"
    ngStyle]="{backgroundColor: odd % 2 !== 0 ? 'yellow' : 'transparent'}"
    *ngFor="let odd of oddNumbers">
  {{ odd }}
  </li>
</div>

// in .ts file
export class AppComponent {
  oddNumbers = [1, 3, 5];
  onlyOdd = false;
}

```

#### `ngClass` and `ngStyle` recap

The `ngStyle` is used to set a given DOM element style properties. For example:
```
<div [ngStyle]="{'background-color':'green'}"></<div>
```
The `ngClass` is used to set the CSS class dynamically for a DOM element.

```
<li
  class="list-group-item"
  ngClass]="{odd: even % 2 !== 0}"
  [ngStyle]="{backgroundColor: even % 2 !== 0 ? 'yellow' : 'transparent'}"
  *ngFor="let even of evenNumbers">
    {{ even }}
</li>
```

#### Attribute directive

Create a basic attribute directive by: `ng g d basic-highlight`. 

```
import { Directive, OnInit} from '@angular/core';

@Directive({
  selector: '[appBasicHighlight]'
})
export class BasicHighlightDirective implements OnInit {
...
}
```

#### the Renderer

#### HostListener to listen to host events

#### HostBinding to bind to host properties

#### Binding to directive properties

#### Build a structural directive

#### `ngSwitch`

## Section 8: Course Project 3 - Directives

Add a dropdown directive typescript file and update the dropdown buttons.

## Section 9: Using Services & Dependency Injection

Services are to provide common functionalities to various modules. 

#### Assignment 5 (section 9): practicing services

## Section 10: Course Project 4 - Services & Dependency Injection

Add a recipe service which combines some functions and hinds the data. Use `@Injectable()` in `recipe.service.ts`. That is, `RecipeService` is an injeactable service, while the `ShoppingListService` is the dependency.

## Section 11: Changing Pages with Routing 

## Section 12: Course Project 5 - Routing

## Section 13: Understanding Observables 

Angular Observable use as an interface to handle a variety of common asynchronous operations. For example, to send observable data from child to parent component by defining custom events, handle AJAX or HTTP requests and responses, listen and respond user input in Angular Router and Forms. 

> Observables are declarative—that is, you define a function for publishing values, but it is not executed until a consumer subscribes to it. The subscribed consumer then receives notifications until the function completes, or until they unsubscribe.

> RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using observables that makes it easier to compose asynchronous or callback-based code.

Reference: 
1. [Link djamware](https://www.djamware.com/post/5da31946ae418d042e1aef1d/angular-8-tutorial-observable-and-rxjs-examples)
2. [Link Angular Doc](https://angular.io/guide/observables)

## Section 14: Course Project 6 - Observables

Refactor the code using `observable`.

## Section 15: Handling Forms in Angular Apps

## Section 16: Course Project 7 - Forms

Using `Forms` for the edit button. 

To make sure the amount valid, use the pattern matching: `pattern="^[1-9]+[0-9]*$"`

## Section 17: Using Pipes to Transform Output

## Section 18: Making Http Requests

## Section 19: Course Project 8 - Http

## Section 23: Deploying an Angular App

## Section 31: Course Roundup