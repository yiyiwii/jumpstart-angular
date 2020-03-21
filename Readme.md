# Angular Jumpstart

-- Learning note of Udemy course: [Angular - the complete guide] (https://www.udemy.com/course/the-complete-guide-to-angular-2)

## Section 2: The Basics

### Component

It is actually a class. In the code, it is a sub-folder inside `app` folder. It includes (`.ts`, `.html`, `css`) files. 

Creat new component (Assignment 1, practicing components):
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

#### Property Binding vs String Interpolation

Use `[]` to bind property. 
```
<button class="btn tn-primary" [disabled]="!allowNewComponent">Add Server</button>
<p [innerText]="allowNewServer"></p>
```

#### Event Binding

```
<button 
class="btn tn-primary" 
[disabled]="!allowNewComponent" 
(click)="onCreateServer()>Add Server</button>
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

#### `ngIf`, output data conditionally 
```
<button class="btn btn-primary" (click)="showSecret = !showSecret">Display Details</button>
<p *ngIf="showSecret">Secret Password = tuna</p>
```

#### `ngStyle`, style elements dynamically

#### `ngClass`, apply CSS classes dynamically

#### `ngFor`, output Lists

#### Assignment 2: Databinding

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

## Section 6: Course Project 2 - Components & Databing

## Section 8: Course Project 3 - Directives

## Section 10: Course Project 4 - Services & Dependency Injection

## Section 12: Course Project 5 - Routing

## Section 14: Course Project 6 - Observables

## Section 16: Course Project 7 - Forms

## Section 19: Course Project 8 - Http

## Section 23: Deploying an Angular App

## Section 31: Course Roundup