---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Angular
info: |
  Presentation slides for MIAGE UNA students.
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# Angular

Apprendre les bases

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/anohabbah" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
transition: fade-out
---

# C'est quoi Angular ?

Framework de développement web

- 🧑‍💻 **Develop faster** - Angular CLI, build, test and serve
- 📝 **Open Source** - Built with transparency
- 🎨 **Support by Google** - Big tech product
<br>
<br>

Lire plus sur [Angular.dev](https://angular.dev/overview)


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: cover
background: https://cover.sli.dev
class: text-center
---
# Les fonctionnalités d'Angular
Ce qu'on peut faire avec Angular
---
transition: slide-left
level: 2
---
# TypeScript
Fonctionnalité d'Angular

JavaScript code :
```js
function add(a, b) {
  return a + b
}
```

TypeScript code :
```ts
function add(a: number, b: number): number {
  return a + b
}
```

TypeScript = Type + JavaScript

<!--
Le code est entièrement écrit en TypeScript (libre et ouvert sur github)

Angular va s'appuyer fortement sur les fonctionnalités de TypeScript tel que les décorateurs.
-->
---
layout: two-cols-header
layoutClass: gap-16
transition: slide-left
---
# Components
Fonctionnalité d'Angular

Les composants sont des morceaux d'UI autonomes et réutilisables.

```shell
ng g c my-component
```

::left::

app.component.ts
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'app';
}
```

::right::

app.component.html
```html
<h1 class="title">{{ title }}</h1>
```

app.component.css
```css
.title {
  color: red;
}
```

---
transition: slide-left
---
# Dependency Injection (DI)
Fonctionnalité d'Angular

L'injection de dépendance ou inversion de contrôle (IoC) est un modèle de conception dans lequel une classe accepte
les dépendances par l'injection de constructeur, par les arguments de factory method, ou par injection de propriété.

```ts
import { Component } from '@angular/core';
@Injectable()
export class MonService {
    data = [];
}
```

```ts
import { Component, inject } from '@angular/core';

@Component({
  selector: 'app-root',
  template: '<h1>DI</h1>'
})
export class AppComponent {
    readonly monService = inject(MonService);
    
    constructor(private monService: MonService) {}
}
```

---
transition: slide-left
---
# Modules
Fonctionnalité d'Angular

Angular modules are a way to group components and other resources together:

<div grid="~ cols-2 gap-2" m="t-2">
```
/
|-- src
|   |
|   |-- app
|   |   |-- shared
|   |   |   |-- shared.module.ts  <---- This is the module
|   |   |   |-- shared.component.ts
|   |   |   |-- shared.component.html
|   |   |   |-- shared.component.css
|   |   |-- app.module.ts  <---- This is the module
|   |   |-- app.component.ts
|   |   |-- app.component.html
|   |   |-- app.component.css
```

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  exports: [
    SharedComponent
  ],
  declarations: [
    SharedComponent
  ]
})
export class SharedModule { }
```
</div>
---
transition: slide-left
zoom: 0.7
---

# Pipes
 Les fonctionnalités d'Angular

 Pipes are a way to transform data in your application

```sh
npx ng g pipe my-pipe
```

<div grid="~ cols-2 gap-2" m="t-2">

<div>

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'myPipe'
})
export class MyPipe implements PipeTransform {
  transform(value: any): any {
    return value;
  }
}
```

```html
<p>Total: {{ amount | myPipe }}</p>
```
</div>

<div>
<h1> Built-in Pipes</h1>
<ul class="list-disc">
<li>AsyncPipe</li>
<li>CurrencyPipe</li>
<li>DatePipe</li>
<li>DecimalPipe</li>
<li>I18nPluralPipe</li>
<li>I18nSelectPipe</li>
<li>JsonPipe</li>
<li>KeyValuePipe</li>
<li>LowerCasePipe</li>
<li>PercentPipe</li>
<li>SlicePipe</li>
<li>TitleCasePipe</li>
<li>upperCasePipe</li>
</ul>
</div>
</div>

---
layout: two-cols-header
layoutClass: gap-16
transition: slide-left
---
# Forms
Fonctionnalité d'Angular

Handling user input with forms

::left::
Template driven approach

```ts
import { Component, signal } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-template-favorite-color',
  template: `
    Favorite Color: <input type="text" [(ngModel)]="favoriteColor">
  `,
  imports: [FormsModule],
})
export class FavoriteColorTemplateComponent {
  favoriteColor = signal('');
}
```

::right::
Reactive approach

```ts
import { Component } from '@angular/core';
import { FormControl, ReactiveFormsModule } from '@angular/forms';

@Component({
  selector: 'app-reactive-favorite-color',
  template: `
    Favorite Color: <input type="text" [formControl]="favoriteColorControl">
  `,
  imports: [ReactiveFormsModule],
})
export class FavoriteColorReactiveComponent {
  favoriteColorControl = new FormControl('');
}
```

---
transition: slide-left
---
# HTTP Client
Fonctionnalité d'Angular

Communicating with backend services using HTTP.

```ts
@Injectable({providedIn: 'root'})
export class ConfigService {
  private http = inject(HttpClient);
  // This service can now make HTTP requests via `this.http`.


  getConfig(): Observable<Config> {
    return this.http.get<Config>(`/api/config`);
  }
}
```

---
layout: two-cols-header
layoutClass: gap-16
transition: slide-left
zoom: 0.65
---
# RxJS
Fonctionnalité d'Angular

RxJS is a library for reactive programming in JavaScript.

::left::

ReactiveX combines the **Observer pattern** with the **Iterator pattern** and **functional programming** with collections to fill the need for an ideal way of managing sequences of events.

The essential concepts in RxJS which solve async event management are:

- **Observable**: represents the idea of an invokable collection of future values or events.
- **Observer**: is a collection of callbacks that knows how to listen to values delivered by the Observable.
- **Subscription**: represents the execution of an Observable, is primarily useful for cancelling the execution.
- **Operators**: are pure functions that enable a functional programming style of dealing with collections with operations like `map`, `filter`, ``concat``, ``reduce``, etc.
- **Subject**: is equivalent to an EventEmitter, and the only way of multicasting a value or event to multiple Observers.
- **Schedulers**: are centralized dispatchers to control concurrency, allowing us to coordinate when computation happens on e.g. setTimeout or requestAnimationFrame or others.


::right::
Normally, you register event listeners:
```js
document.addEventListener('click', () => console.log('Clicked!'));
```

Using RxJS you create an observable instead:
```ts
import { fronEvent } from 'rxjs';

fromEvent(document, 'click').subscribe(() => console.log('Clicked!'));
```

React on observable, using operators:
```ts
import { fromEvent, throttleTime, map, scan } from 'rxjs';

fromEvent(document, 'click')
  .pipe(
    throttleTime(1000), // emet une valeur et ignore les autres pendant 1 seconde
    map((event) => event.clientX), // transformation: récupérer le clientX
    scan((count, clientX) => count + clientX, 0) // faire une somme de tous les clientX reçus
  )
  .subscribe((count) => console.log(count));
```
---
layout: image-right
image: https://cover.sli.dev
class: text-center
---

<div class="w-full h-full flex items-center justify-center">
<h1>Demo</h1>
</div>

---
layout: end
---
