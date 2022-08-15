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







   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 




























