ng new nombre-proye   ->create
ng serve --port 4201  ->to change port
with CLI you can create scaffolding of components, directive,services and others

FOLDER ESTRUCTURE
/ root path
package.json(npm descriptor dependency)
.gitignore(file to ignore files folders)
`src:` in specify app ->  source code of our project
 	index.hmtl ->ini page
`dist:` folder content all files compiled, is the version of your app load to web server
`public:` here you put static files like images and otheres, more know as assets, these files also move to "dist" folder
`e2e:` is for test development, come from end to end testing
`node_modules:` they are the files dependencies that we mantence with npm
`tmp:` it's a folder that we don't touch, it has temporary files that angluar CLI generate with is doing anything
`typings: ??`

ANALYSIS OF FILES

## /src/index.hmtl  
				content a component <app-root> </app-root>  there are a components tree, this is the root component
                 in all project you find many components, these components build your app
				 Webpack inject JS into html
 ## main.ts
- there are two kind of imports
1. import dependencies to external libraries
	they are other projects code, managed by npm in package.json as:
		`import{enableProdMode} from '@angular/core';`
    its code is in node_modules

2. import to own project code
	`import{AppModule} from './app/app.module';`  it's not necesary put the extension

	
finally ther is a final line code
`platformBrowserDynamic().bootstrapModule(AppModule)
.catch(err => console.log(err));`

 this is the bootstrap, the start of app, it say what Angular made to give life to app
 when invoke start system we indicate what is the main module of app(AppModule) and who have the necesary components to run
finally, bootstrap made that Angular read the module code and know what component exists into index

`app.module.ts`

 in all imports inside main.ts there is one fundamental, it's app.module.ts main module
 in this main module app.module.ts, here we found the several imports comming another modules
 there are two keys things to know the flow ejecution
`import our root component`
 in the main module app.module.ts, we foud the import to aplication root component(that tag no HTML standard inside index.html BODY)
 `import{AppComponent} from './app.component';`

 this is an important component in this point because is the first one we use and created by CLI
 its a reference to AppComponent here will be the class created to implement component 

`Decorate @NgModule`

the Decorate is implements by TypeScript
allow insert metadata to functions,classes
it has a name and use it to assign those data
it would can be change the comportamiento that we decorated

@NgModule({declarations:...imports:... providers:...}) 

this contain an object pass as parameter, here we edit and add new things
it contain a property called "bootstrap" an array with componets that Angular Run give life
this say to Angular there is a compoment inside index.html implements with AppComponent that need to execute.

` root component`
 we use in index.html
 <app-root></app-root>

in app.component.ts
 @Component({
 	selector:
 	templateUrl:
 	styleUrls:
 })  

 * selector or label that implement this componente: "app-root", use in index.html
 * file .html its template "./app.component.html"
 * styles use this component "./app.component.css"

 `Sumary execution flow Angular`
 1. in the index.html we have a root component called "app-root"
 2. when we execute (ng serve) Webpack tool generate the packages(bundles) and put scripts into index.html
 3. Webpack begin with main.ts
 4. in main.ts we found an import to main module(AppModule) and call to Start system(bootstrapModule) it contain the main module of app as parameter
 5. in main module(app.module.ts) import the root component(AppComponent) and in decorate @NgModule indicate this component belongs to bootstrap
 6. the component root code has the selector "app-root", label exists in index.html
 7. the template in the root component has the HTML show when we run the app


 `ANALYSIS MAIN PROJECT ANGULAR`

 `package.json`
  here we declare dependencies of our aplication managed by npm, its code is in JSON
  the property "dependencies" has the Angular library with several modules like "common","compiler","core",etc
  `main component of the app`
  <mi-nompre-proyecto-app> </mi-nompre-proyecto-app>
  this is the root component of our app  locate in src/app
  initial we can see .html contain view of this component and a .css
  if your componente named "my-nam-proj-app" these files will be "my-nam-proj.component.html" and "my-nam-proj.component.css"

`ANGULAR COMPONENTS`
 
 It all starts with at least one component
 our App will has a component tree (dad,son,etc)
 components are like new HTML labels we created acording to our needed, like a navegation section or a form label
 to define our label, for example, the component use a little HTML with CSS offcourse and JS to define functionality
 
 `LOCATE INITIAL COMPONENT`
 when you open the index.html locate in "src" we see the tag <app-root> this is the main component the root of the tree

 `UNDERSTAND COMPONENT CODE`
 the code is in "src/app"
 name-proj.component.html: equivalent to "View" in MVC architecture
 name-proj.component.css: allow put styles 
 name-proj.component.ts: is TypeScript file and it will translate to JS, equivalent to "controller"
 name-proj.component.spec.ts: TS file to testing tasks
 
 .component.html or the view allow all HTML code and use components, stringInterpolation{{}} 
 if you have a variable like this {{var_a}}, this var is coming from proj-name.component.ts if you open will find:
 	* import "component" from @angular/core
 	* decorate function @Component that made the action to register component
 	* the Class, turn it self like a "controller"

 decorate function has:
 "selector", label to tag (component)
 "templateUrl", .html of the component 
 "styleUrls", css array we needed

 in the class of component, we will put an export before class
 here we add all properties and methods we need to use from "view"   
 export class AppComponent{
 	"properties & methods"
 }

`SINTAX FOR ANGULAR VIEWS`
 - expressions, binding to properties, event managedment and double binding
 what we can declare in a view?
 - Property: any value that we asign by one atribute of Html, it can be a simple html atribute or personalized
 - Expression: content of label, is a declaration tha Angular will process and replace by it value
 - Binding: its a link between Model and View, also exists double binding, values are reflected in booth sides
 - Event: it posible define managedment,they are functions 

`INFORMATION FLOW FROM VIEW TO MODEL AND VICEVERSA`
 - programer define for what way the flow information pass from view to model or model to view.

 from Model-View: [property] {{expresion}}
 from View-Mode:[(ngBinding)] (event)

1. property has a flow from model to view, we use brackets [property]
2. expresion also goes from model to view, we use double curly braces {{expression}}
3. binding or double Binding goes in two ways model to view and view to model, we use [(ngBind)]
4. goes from view to model, generaly is for execute metods, we use (event)


 example, use property and expression
 <a [href]="m_link"> link as PROPERTY</a>

 <a href={{m_link}}> link as EXPRESSION</a>

`COMPONENT`
- is the most important part of Angular
- allow structure the app, encapsular functionality, easy mantencies


`Component tree`
 - an Angular APP is development with components
 - generaly we have a component tree with a father first
 - in our tree is posible the first block contain
 	* tool bar, nav bar, menu etc
 	* a main part with display all "windows" of our app
 	* login area
 then, each main component will can sub-divide in new components

 we can componentizar from component to sub-component so far, but if we have a lot of sub-component it has consuption resources

 `Component Vs Directives`
 
 components are part of bussines
 Directives we use to presentation and structural issues

 you can think in a compopent like a container to solve a needed, UI to interact, data list, a form, etc
 in documentation a component is a directive type
 there are 3 types:
 Components: it's a directive with a template
 Attribute Directives: change look or behavior of element
 Structural Directives: do change in DOM, add,delete,management elements: ngFor ngIf

 `Components Part`
 - a Template   -> templateUrl  as view
 - a Class      -> as controller
 - a decorate function  -> as component register join  JS & Html

 `Component Decorator`
 - its a declaration how will be a component and its parts
 - its a implementation of software design pattern
 - extend a function by other function
 - receive a function as argument and return it with aditional functionality
 - start with "@" then its name
 - we decorate a function, a class poperty, a class, etc
 - look at the first line
  * import{Component} from '@angluar/core'
 - Import is carrying the Component Class
 `what information we append with a Decorator` 
  -Angular use Decorator to register a component
  -Add information to recognize by another parts of app
	@Component({
	moduleId: module.id,
	selector: 'test-angular2-app',
	templateUrl: 'test-angular2.component.html',
	styleUrls: ['test-angular2.component.css']
	})
	
	- it contain anotations we give "metadata"
   `moduleId:` for resolve relative Urls.
   `selector:` its the new tag Name we created and use in HTML
   `templateUrl:` the HTML file it contain the view code
   `styleUrls:` its an Array of CSS
   
   Important, All of these, area created by Angular CLI with a scaffolding
   
   `CREATE A NEW COMPONENT` 
   - in the root of app write
    ng generate component componente-name or ng g component component-name
   - in adition of component we generate scaffolding like directives,services,clases,etc
   - the new files are in "src/app"
   - this file has you should know
    * Imports
    * Component decorator
    * Class like a controler we export

    Also an implements
    export class component-name implements OnInit

 implements is an interface, it say we use a function ngOnInit
    in this function we put code will be execute 
 - we use this componente in the html created with this
 
  `use this new component`
   1. import component code from component you needed
     in app.component.ts
     import {nameComponent} from './component-name'
   2. declare you will use this component, from parent  app.component.html 
     <app-first-component> </app-first-component>
	
 `BASIC MODULES`
  - its a union among components and other artifacts like directives
  - its a main element we can organize the code app
  - instead of put all components code, directives in the main module, its recomendable 
    have many modules and group them in diferent elements

  `create a module`
   ng generate module module-name

  - it created inside "src/app" a subfolder with the same name of module
  - content of name-module.module.ts
    @NgModule({
      imports:[],
      declarations:[]
    })

  - as you can see we have
  * imports: imports this module needed
  * declaration: with components, or artefact this module build

  `Generate a component inside module`
  - just here all components was create inside main module,
  - but if we create in a diferet subfolder we will need:
    
    ng generate component folder-module/name-new-component
   
   this generate a subfolder inside module we have specify
   folder-module
    name-new-component(folder)   
 
 `Export module out`
  - if we want to export to use in another modules we will add information to Decorator module: export array
  - supose "second-component" we want it will can use from another modules, add component Class name in array "exports"

 @NgModule({imports:[] ,declarations:[],  exports[name-new-component]}) 

 `Use component in other modules`
 - modify main module to know component in the new module
 - import entire module we created, because this module contain the component we exported
 
  import {ModuleName} from './folder-module/new-module.module'
 - import of our new module will be declarate in "imports" property of main module
 main module:
  @NgModule({
    declarations:[],imports:[BrowserModule,Name-new-module],etc
  })

  `use component in HTML`
  finally we use component, we put in root compoment the component selector from new component created
** ALERT REVIEW MODULE AND COMPONENT CREATED** THIS PART IS SO-SO 
 
 `ANGULAR ESSENTIALS DIRECTIVES`
 `ngClass Directive`
 - it allow us modify CSS
 - from Angular 2 directives are to solve specify needed to manage DOM and others
 - pay atention, it's not necesary resolve all Class issue with ngClass
 
 `assign CSS class with ngClass`
  - we can use many values to express classes group 
  <p [ngClass]= "['negativo','off']"> it can be apply many classes </p>
  <p [ngClass]= "arrayClases" > it can be apply many classes </p>
  - in TS
   clases = ['positivo','si'];

   - a object with properties and values, each prop name is a posible CSS class
   <li [ngClass]="{positivo:cantidad >0,negativo:cantidad <0, off:desactivado, on:!desactivado}">linea </li>
  
  HTML
  <p>
    <button
    [ngClass]="{si:estadoPositivo,no:!estadoPositivo}"
    (click)="cambiarEstado()"
    >{{texto}}
    </button>
</p>
  
  TS
  texto:string="SI";
  estadoPositivo:boolean=true;
  cambiarEstado(){
    this.texto =(this.estadoPositivo)?"NO":"SI";
    this.estadoPositivo=!this.estadoPositivo;
  }

 CSS
 button {
    padding: 15px;
    font-size: 1.2em;
    border-radius: 5px;
    color: white;
    font-weight: bold;
    width: 70px;
    height: 60px;
    }
    .si{
    background-color: #6c5;
    }
    .no{
    background-color: #933;
    }

  `ngFor DIRECTIVE`
   - for loop

  `*ngFor="let pregunta of preguntas"`
  - `*` it's a nomenclature to indicate us it affect to DOM (insert, managed,delete)

 `loop arrays with objects`
   <p *ngFor="let objPregunta of preguntasObj">
    {{objPregunta.pregunta}}:

`to modify we implements interfaces TS`
 - in this case we use to declare a data type and editor will help us when we write
 - its recomendable create separate and import in our component


  `ngModel DIRECTIVE`
  - Basically is a link between model and view (TS & html)
   ejm, we have a component
   export class CuadradoComponent{
    lado=4;
   }

   if we want to use "lado" in a input 
  <input type="number" [ngModel]="lado">

   we are using ngModel directive as a property INPUT field

   `declare ngModel`
   - we need import "FormsModule" from component we want to use directive

    import { NgModule } from '@angular/core';
    import { CommonModule } from '@angular/common';
    import { CuadradoComponent } from './cuadrado/cuadrado.component';
    `import { FormsModule } from '@angular/forms';` 
   
    @NgModule({
    imports: [
    CommonModule,
   `FormsModule`
    ],
    declarations: [CuadradoComponent],
    exports: [CuadradoComponent]
    })
    export class FigurasModule { } 


    - two important things:
     1. import FormsModule  from @angular/forms
     2. declare into array's import

  `link double binding`
     -we use "banana in a box"
     <input type ="number" [(ngModel)]="lado">
    - now if we write in view this travel to model


  `ngModelChange Event`
    - it's similar like double binding   
    - we need a method into component it get de var "$event" 
    <input type="number" [ngModel]="lado" (ngModelChange)= "cambiarlado=($event)">
  
  `Binding in detail`  pag.68
  `interpolation{{}} in detail`
  
  `string interpolation`
  - it's a form to replace a expression for a value
   <img src="{{urlImagen}}">
  - all expression become in string before use it in template

  {{somString}}
  {{1+1}}
  {{!boolean}}
  {{componentMethod()}}

  - Bindings cannot contain assignements
   {{expr=1}}  error
  - can't write control sentences if, for etc
  - dont' call API REST in a expression
  - be simple

  `binding to properties`
   -its for assign a value to an element property
   -it can be a literal value

   `Component Properties`
   - components generated with Angular are implemented using a class (POO)
   - properties of that class (data) are called "component properties"
   - in this article we also reference a component expresed in a template as html properties(DOM) or in gral component properties.

   `properties expressed in a template`
   - in component's html (template or view) properties are any values we assign by binding
    ejm
    normal
    <img src = "imagen.jpg">
    <button disabled> im disactivated</button>
   
   with binding
   <img [src]="rutaImagen">
   <button [disabled] ="estadoBoton"> im activate or not </button>

   binding [], values are called from component "rutaImagen" such as "estadoBoton"

   - important to know, when you work with template properties, you're not set html atributes, with [] it becomes in Angular properties.

  `property binding variant`
   - we can set binding to directives properties
   <div [ngStyle]="objEstilos">DIV con estilos definidos por Angular </div>

   - also set personalized properties to our components
    <mi-componente [propiedadPersonalizada]="valorAsignado"></mi-componente>
    this is a special case, we will see in @Input properties of components
    -we can create any component propertie
     parent component-> "valorAsignado"        (review again ñ_ñ both)
     son component-> "propiedadPersonalizada"

  `one-way bindig`

  - assign a property is dinamic, if changed also change what we binding
  - property binding is one direction from father to son

  `posible values for property`

  - normally is  binding by component propertie, but we put another TS code
  - we can bindig to a literal
 
  <img [src]="'ruta.jpg'">
  in this case ruta.jpg is writed between simple comillas, so is a literal. Angular evaluate it as String

 also we can binding to a method, result of method aply to binding property
 <p [ngClass] ="obtenerClasess()"> this get a class returned by method </p>

 `avoid lateral effects`
 - avoid when we evaluate a property value it change component state
 - ejm


 <img [src]="ruta = 'ruta.jpg'">
 it can't do
 - pay atention, when we bindig a property by return value method, Angular doesn't show errors if we modify compoment state
 <img [src]="calculaSrc()">

 `Binding to properties Vs String interpolation`
its similar but different lets see


first, it use interpolation asign to src value inside {{}}
second, it bind to property src with urlImagen between "" which one is the correct?
other Example

<li [class]="valorClass">item 1
item 2
<p>{{texto}}</p>
<p [innerHTML]="texto"></p>
- first paragraph we put text by interpolation
- second paragraph is the same text but by innerHTML component property

`interpolation with string`
- pay atention there is no problem use each one but you define with your team
- advice is use string interpolation fro string text

`use property binding with diferent values to strings`
example 
button property "disable" should be a binding property to boolean value 

correct way
<button [disabled]="activo">Clic aquí</button>

incorrect,  result maybe is not we want
<button disabled="{{activo}}">Clic aquí</button>

{{activo}} interpolate by "false" word, disabled="false", in HTML si similar to putt disabled without value
 
 - if the value is not a string use property binding

<div [ngStyle]="estilo">Test de estilo</div>

`depure strings in Angular templates`
- if we use property binding also string interpolation, there is a diference with depure before.

 cadenaXSS='this is a <script>alert("test")</script> con XSS'

there is a problem with code injection, we use instead of
<div>{{ cadenaXSS }}</div>
<div [innerHTML]="cadenaXSS"></div>

- Angular make a healt of string, disabled Script label,
 
 " this is a <script>alert("test")</script> con XSS Esto es un alert("test") con XSS "

 in this case script is a text and not a label

`Binding to atribute`

 - its easy to implement.
 - we start what is attribute and property

`what is attribute in Angular`
- we define it in Angular context, ok let's go
- many times we use "atribute" as a sinonomous of "property"
- "id" attribute in HTML is property "id" of DOM, but there is attributes has not direct map to DOM like "colspan"
- there are also HTML attributes that map to DOM properties than are not called and executed in the same way as "class" "classList" 
- when we do property binding we have elements properties, but we don't have attributes
- we can do this

 <div [id]="idDivision">Test de binding a propiedad</div>
 but not this
 <td [colspan]="1 + 1">test</td>
- also, we can't do this neither
<td colspan="{{1 + 1}}">test</td>

- we use both(SI and PB ) only properties defined in Angular and doesn't in HTML attributes.

`syntaxis to bindig an attribute` (pg.82)
- we use "attr" then attribute name betwen brackets[]
<td [attr.colspan]="1 + 1">test</td>

- to bind "data attribute"
 <div data-cliente="desa-web"> desa web</div>
- in TS
  cliente={
    name:'DevelopmentZone'
  }

  <div [attr.data-cliente]="cliente.name">({cliente.nombre}) </div>
  `complete Example`
- this example show how bind to attribute
- its a componente that show us polygon dots 
  name|sides|dots
  square|4|[10,5|15,5|15,10|10,10]
- in component we create a obj
  
  poligono = {
    nombre: 'cuadrado',
    puntos: [
    {
    x: 10,
    y: 5
    },
    {
    x: 15,
    y: 5
    }]}
  - in html , here is the key [attr.]
  <th [attr.colspan]="poligono.puntos.length">Puntos</th>

 `Template statements`
 - sentece to execute as response an event its called "statement"
 - its normal that statement run a method, like press a button
 - but also contain the sentence into template
 <div (click)="cliente.nombre = 'DesarrolloWeb.com'">Marcar Cliente</div>
 - statement is declared between quotation marks
 - statements can modify components properties
 - its not allowed
  * new operator
  * increase decrease (++ --)
  * +=
  * pipes

`context statements`  (pg.86)
 - this object $event give us info about event created
 <button (click)="procesarEvento($event)">Transmito el objeto evento</button> 
 - $event is important because allow send util data
 - advice to use statements
  * define statement in compoment method

  `COMUNICATION BETWEEN COMPONENTS with @Input`
  - we use @Input decorator
 
  - father to son

  * in father component TS put dato to send son

   cliente={
    nombre:"pinche",
    cif:"123",
    direccion:"adress of pinche"
    }
   * in father view html put call son
    <app-comunication-son
    [nombre]="cliente.nombre"
    [cif]="cliente.cif"
    [direccion]="cliente.direccion"
    >
    </app-comunication-son>

    <button (click)="cliente.cif='ESB9922'">Cambiar CIF</button>


    
    * in son component use import { Component, OnInit, Input } from '@angular/core'; and put this in class 

    @Input()
    nombre = 'DesarrolloWeb.com';
    @Input()
    cif!: string;
    @Input()
    direccion!: string;
 
   * in view what data we render
     <p>
        son_Nombre: {{nombre}}
        <br>
        son_Cif: {{cif}}
        <br>
        son_direccion: {{direccion}}
    </p> 
 
  `personalized event with @Output` (pg.92)
 
  - son to father

  * in son component import { Component, OnInit, Output, EventEmitter } from '@angular/core';
  mensaje:string="";
  
  @Output()
  propagar = new EventEmitter<string>();  
  
  onPropagar(){
    this.propagar.emit(this.mensaje);
  }
  * in son view
  <p>
    <input type="text" [(ngModel)]="mensaje">
    <button (click)="onPropagar()">Propagar</button>
  </p>
  
  * in father component 
  procesaPropagar(mensaje:any) {
    console.log(mensaje);
    }

 * in father view, put call to son comp
  <app-son-to-father-son
      (propagar)="procesaPropagar($event)"
  >
  </app-son-to-father-son>

 `ANGULAR SERVICES`
 
 
 




























