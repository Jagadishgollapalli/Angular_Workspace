# Start

> Roadmap:

---

1. Project Structure
2. Components
3. Data Binding
4. Component communication
5. Directives
6. Routing
7. Forms: Template driven and Reactive

---

> Installation

---

1. Make sure node js is installed. [node -v]
2. Install angular CLI. [npm install -g @angular/cli] -g installs it globally.
3. ALl angular commands starts with 'ng'. To check version [ng --version]
4. Create angular application [ng new Appname]
5. Run Application [ng serve / npm start] [ng serve -o] : opens the application by default [ng serve -p XXXX] opens in a specific port that we give

---

> Introduction

---

Angular Component:

1. Its a combination of HTMS, CSS, .ts and test file.
2. 4 Major components of webpage: Header, Side nav, Body, Footer. Each having a separate component.
3. In .ts file, @component decorator is used and it converts a js file into a typescript file.
4. template url links html file to the component.
5. style url links the style sheets to the component. An array of paths to the various css files
6. Entire app module is wrapped with Bootstrap component.

---

# Concepts

> Data Binding

---

1. ONE WAY DATA BINDING

   - String Interpolation - One Way Data Binding - How we can access - `{{}}`
   - Property Binding - One Way Data Binding - How we can access - `[]`
   - Class Binding - One Way Data Binding - How we can access - `[class]`
   - Style Binding - One Way Data Binding - How we can access - `[style]`
   - Event Binding - One Way Data Binding - How we can access -
     - Ex: Button `(click)= "increment()"`
     - Ex: Input `(input)= "ChangeName($event)"`

2. TWO WAY DATA BINDING - Import formsModule into app.module.ts
   - Syntax: `[(ngModel)] = propertyname(variable)`
     - Ex: `<input type="text" [(ngModel)] = "city">` - in Html file, so it will automatically change in TS file.

## Directives

> Definition: _`Directives are custom HTML attributes which tell angular to change the Structure, Style or behavior of the DOM elements.`_
>
> 1. Types - Structural directives, Attribute directives, Component directives.

---

    1. Structural directive

       1. NgIf - For Condition

       (Ex: show:boolean =  false | in TS File
       <h1 *ngIf="show"></h1> | in HTML File)

       2. NgFor - For loops

       (Ex: <tr *ngFor="let m of movies">
       <td>{{m}}</td></tr>) | in TS File , movies:[] = ["","","","",""]

       3. NgSwitch

       (Ex: num1:number = 2, num2:number: 3, op:string = "+" | in TS File
       <div [ngSwitch] = "op">
       <div *ngSwitchCase="'+'">{{num1+num2}}</div>
       <div *ngSwitchCase="'-'">{{num1-num2}}</div>
       <div *ngSwitchCase="'*'">{{num1*num2}}</div>
       <div *ngSwitchCase="'/'">{{num1/num2}}</div>
       <div *ngSwitchDefault="''">Invalid Match</div>
       | in HTML File
       </div>
       )

## Pipes

> Definition: _`Used to transform data before displaying it on in the browser, pipes take the data as input and format the data to some form`_

---

    - Syntax:  `Expression | pipename[:parameters]`
    - Built in pipes:
        - CurrencyPipe
        - DatePipe
        - DecimalPipe
        - JsonPipe
        - LowerCasePipe
        - UpperCasePipe
        - PercentPipe
        - SlicePipe
        - AsyncPipe

    Example: salary:number = 67000; | in TS File
    <h1>{{salary |  currency : 'INR': 'symbol'}}</h1>

---

- Custom Pipes
  - command: `ng g p test`
  - import TestPipe into app.module.ts and add it to declarations.
  - customize your pipe to return something

## Template Reference

> Definition: `Template Reference Variable in angular is used to access all the properties of any element inside the DOM. It can also be a reference to an Angular component or directive or web component. Template Reference Variable can refer to the following: DOM element. Directives.`

---

HTML File

```
<input type="text" placeholder="Enter Email" #e value="abc@gmail.com">

<button (click)="updateEmail(e.value)">Update</button>
<div #d class="one two" id="special>{{email}}</div>

<div>{{d.classList}}</div>
<div>{{d.id}}</div>
```

TS File

```
email:string = "";
updateEmail(ip){
    this.email = ip
}
```

## Decorators

> Definition: `They are useful to data passing between the components or we can say we have decorators for parent and child communication`

---

# Input Decorator

<u>app.component.ts</u>

```
Declare :  fullName:string = "Jane Smith";
```

<u>app.component.html</u>

```
<app-child [d1]="fullName></app-child>

In Header component
```

<u>header.component.ts</u>

```

1. @Input() d1;

Now, we can use this variable in Header component html file

<u>header.component.html</u>

{{d1}}  OP: Jane Smith
```

# Output Decorator

<u>header.component.ts</u>

1. Output Decorator

```
import {EventEmitter, Output} from "@angular/core";

@Output() customEve = new EventEmitter();

message:string = "Passed to Parent"

passToParent(){
    this.customEve.emit(this.message);
}

```

<u>app.component.html</u>

```
<app-header (customEve)="updatecdata($event)"></app-header>

<u>app.component.ts</u>

declare a variable

cdata:any

```

<u>header.component.html</u>

```
<button (click)="passToParent()">send</button>
```

2. Using Template reference variable

```
Child Component.ts:

data: "This is a Child Component"

In app.component.html we give
<child.component.html #child ></child.component.html>

so using child variable we can access all the data in the child component in parent component

using

{{child.data}}

```

3. @ViewChild(Decorator)

```
import {ViewChild} from "@angular/core" In Parent TS File
import {ChildComp} from "./child/child.component"

@ViewChild(ChildComp) header ->(some  variable) name

test(){
    return this.header.passToParent()
}
```

# DOM Manipulation

- we have a property called nativeElement, so we access using this.variableName.nativeElement.style.backgroundColor = "blue";

# View Child vs View Children

Example:

- If we have one `<p #para>Hi, How are you?</p>`, we can access DOM using

```
@ViewChild('para') p ;
console.log(this.p.nativeElement.innerText == "I am good!");
```

- If we have multiple
  `<h1 #heading>Hi, How are you?</h1>`
  `<h1 #heading>Hi, How are you?</h1>`
  `<h1 #heading>Hi, How are you?</h1>`,
  we can access DOM using

```
@ViewChildren('heading') h ;
console.log(this.h._results[0].nativeElement.innerText == "I am good!");
```

## Routing

> 3 key steps : Configuring the routes, Adding router Outlet, Add routing links in template

1. Import RouterModule into app.module.ts from '@angular/router' and store it in imports array.
2. Import Routes also from '@angular/router' into the same app.module.ts

```
Define array const routes:Routes(type) = [
   {
   path: "", component:HomeComponent
   },
   {
   path: "about", component:AboutComponent
   },
   {
   path: "contact", component:ContactComponent
   },
   {
   path:"***", component:NotFoundComponent
   }
]

in the imports: [
   RouterModule:forRoot(routes)
]

in the parent app.component.html
<router-outlet>
</router-outlet>

in the <a routerLink="***" routerLinkActive="active"></a> instead of href, we have to give routerLink="/about" etc.
```

## Services
> Definition: `Angular services provide a way for you to separate Angular app data and functions that can be used by multiple components in your app. To be used by multiple components, a service must be made injectable. Services that are injectable and used by a component become dependencies of that component.`

 #### steps:
        - ng g s test
        - declare the data to be sent to other components inside the TestService class (eg: letters = ["a", "b", "c", "d"])
        - Import test service into app.module.ts
        - inside app.module.ts we have [providers]: [] -> pass TestService = [providers]: [TestService]
        - Inside app.component.ts or any class component, inside constructor() -> constructor(private ts:TestService) 
          /*import TestService into app component*/
        - so we say letters = this.ts.letters
        - In app.component.html
          <div *ngFor = "let l of letters"> {{l}} </div>
        - suppose we have other component, say add.component.html, we have a button in that, and function un ts file to implement
          constructor(private ts:TestService) 
          letters = this.ts.letters
          add(){
            this.ts.letters.push("e");
          }
        - The change will be reflected in the app component as well

# Lyfe Cycle Hooks
  - ngOnChanges() - `Every time we change/ send/ receiving data from parent component to child component, we can log the changes/perform  any task using this Hook.(only executable in child component when data changes not in parent component)`
    - **Imp** `onChanges() - will not be called for property changes or data changes, will be called only for address/reference change happened for variable.`

  - **ngOnInit()** - `when we want to show the data on starting the application, we have to write the requirement in ngOnInit(), not in constructor().`
      - $${\color{red} ngOnInit() vs Constructor()}$$ 
      `Example: when data is coming from parent component to child component, when we call the constructor, the data will not be called, just it initializes the object for that particular component` - so we have use ngOnInit() instead of constructor
      - `Most of the time we use constructor is to implement the dependency injection, ex: when we create a service and use it in the component`

  - ngDoCheck() -  `This life cycle hook runs every time when data changes happen both in parent and child component, not based on the reference or address of the variable`

  - ngAfterViewInit() - ``

  - ngAfterViewChecked()

  - ngAfterContentChecked()

  - ngAfterContentInit()

  - ngOnDestroy()