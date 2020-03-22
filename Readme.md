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

* Interpolation

It uses `{{value}}` inside a UI element. The text between the braces (a template expression) is the name of a component property. 

* Property binding 

Used to bind values to the DOM properties of the HTML elements. Are evaluated on every browser event and any changes made to the objects in the event are applied to the properties. 

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

#### Assignment 2: Databinding

```
<input type="text" class="form-control" [(ngModel)]="username">
<p>{{ username }}</p>
<button
  class="btn btn-primary"
  [disabled]="username === ''"
  (click)="username = ''">Reset User</button>
```

#### Assignment 3: Practicing Directives

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



## Section 6: Course Project 2 - Components & Databing

## Section 8: Course Project 3 - Directives

## Section 10: Course Project 4 - Services & Dependency Injection

## Section 12: Course Project 5 - Routing

## Section 14: Course Project 6 - Observables

## Section 16: Course Project 7 - Forms

## Section 19: Course Project 8 - Http

## Section 23: Deploying an Angular App

## Section 31: Course Roundup