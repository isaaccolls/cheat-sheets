# install

* list available versions: `npm install -g @angular/cli@9.0.7`
* install one: `npm install -g @angular/cli@9.0.7`
* show version: `ng version`

# commands

* new project: `ng new myApp`
* run dev: `ng serve`
* install dependencies: `npm install bootstrap`
* new component: `ng generate component` or `ng g c components/component`

# component

* __template__
  + template
    - html template
    - databinding and directives
* __class__
  + __properties__
  + __methods__
    - views codes
    - ts codes
* __metada__
  + decorator
  + bind view to class

# interpolation

 `{{ value }}`

# directives

* ngIf `*ngIf="expression"`
* ngFor `<tr *ngFor="let var of vars"><td>{{var.a}}</td></tr>`

# data binding and pipes

## property binding

bind values to some element html property `<img [src]="product.imageUrl>`

## event binding

2 ways:

* `<button (click)="ShowImage()">Mostrar Imagen</button>`
* `<button on-click="ShowImage()">Mostrar Imagen</button>`

## two way data binding

FormsModule required, `<input [(ngModel)]="listFilter" name="filter" type="text>`

## pipes

let us proccess and transform data `<p>{{ 'Sample string' | uppercase }}</p>`

* uppercase
* lowecase
* date
* currency
* slice
* etc

### custom pipe

create `ng g pipe product/product-filter --skipTests=true`

# interface

Name convention: always start with capitalize "I" `ng generate interface product/product`

# life cycle

* ngOnChanges
* ngOnInit
* ngDoCheck
* ngAfterContentInit
* ngAfterContentCheced
* ngAfterViewInit
* ngAfterViewChecked
* ngOnDestroy

# decorators

## decorator @Input

``` html
<app-rating-star [rating]="product.rating"></app-rating-star>
export class RatingStarComponent {
@Input() rating:string;
}
```

## decorator @output

``` ts
import { Output, EventEmitter } from '@angular/core';
@Output() newItemEvent = new EventEmitter<string>();
```

# service

fetch data, validations, error warning, etc `ng generate service product/product --skipTests=true`

# essential class RxJS

* observable

``` js
import {
    interval
} from 'rxjs';
const observable = interval(100);
const subscription = observable.subscribe((num) => console.log(num));
```

* observer
* subscription
* operator
* etc...

# routing

[check docs](https://angular.io/guide/router)
