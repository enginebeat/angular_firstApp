Angular Notes

- To create new App 
    ng new appName

- To start dev server
    ng serve

- Then on browser go to
    localhost:4200

- TypeScript is a superset of javascript but will not run in the browser
so it is compiled to javascript

- to install bootstrap
    npm install --save bootstrap

    to use it
        go to angular.json file and on the styles parameter array 
        and before "src/styles.css",
        add "node_modules/bootstrap/dist/css/bootstrap.min.css"

    note that the server will need to be restarted for the changes to take efect

- How is the Angular App started

    It all starts with the file main.ts in the src folder

        platformBrowserDynamic().bootstrapModule(AppModule)
        .catch(err => console.error(err));
    we are passing the AppModule file to the method

    if you then look at the app.component file you will see that 
    in @NgModule we bootstrap the AppComponent module.

    so when starting the angular application the first thing that will run
    is main.ts there we bootstrap the angular application and we pass it 
    appModule as an argument. In this module we tell angular which module to start
    which is the appModule that we defined on app.component.ts.
    Angular then picks all the configuration from that file and renders our app-root
    in index.html.

    - To add our own components after we create them we need to add the name of the component
    to the declarations array in app.module.ts. this is a typescript thing not an Angualr one.


- To create a new component using the Angular CLI
    ng generate component nameOfComponent
    or
    ng g c nameOfComponent

- The CLI should apdate the app.module.ts to import the new component but needs checking

- Component Templates

    normally you declare an external file as the template for your component using
        templateUrl: './app.component.html'
    but you can also embed the HTML strait into the template by using
        template: '<servers></servers><servers></servers>'
    or
    using back ticks to be able to wrap the lines around
        template: 
        `<servers></servers>
        <servers></servers>`

    note that the template is always required, either an inline template or a template 
    pointing to an external file needs to exist.

- As the component templates we can also define the style of the components using
    styleUrls: ['./app.component.css']

    or

    using inline definitions
    styles: [`
        h3 {
        color: dodgerblue;
        }`]


- Component selector

    When creating a component a selector is created for the component. When you 
    add this selector onto the HTML page since that component was registered on the
    app component/ app module it knows what it is and it will rendered it.
    another way of using the selector is using it like an atribute selector

        selector: '[app-servers]'
        or
        selector: '.app-servers'

    now the selector works like a css atribute selector and the html file on the component
    using needs to change to reflect that change

        <div app-servers></div>
        or
        <div class="app-servers"></div>
        depending on which declaration is used above.

----------------------------------------------------------------------------------------------------
                    Data Binding

- String Interpolation
    used by inserting {{aString}} on your HTML wherever you need a variable or even a 
    fixed string inserted. in the javascript code just define this string.

    note that, it has to evaluate to a string but it can be a method, or even a number as it
    will be converted to a string.

- Property Binding
    this is similar to string interpolation but you are acting on the properties of the
    HTML element instead.

        as an example, instead of:  <p>{{aString}}</p> 
        you would use:              <p [innerText]="aString"></p>

    in the case of the property binding it doesn't need to evaluate to a string,
    it needs to evaluate to the value the property is looking for like as an example
    the [disabled] property for a button where it needs to be a boolean. obviously
    a method that returns the property value can also be used.

- Event Binding
    event binding is pretty strait forward, we can bind to any event that the element
    we are binding to ofers by typing on the HTML: 
        
        (event)="method($event)"
    
    so for a button the event can be "click" or for an input can be "input".
    also you can get the data from the event by using the reserved expression "$event"
    this will pass to the method or code the data that the event can return. As an example
    the click event will return the coordinates of where in the page did you click and the
    input will return quit a large object that has a parameter target.value that will give
    you the value of the key pressed.

    note that you can place executable code in between the " " but try to keep it to a minimum.

    as an example you can:
        define the HTML:
            <input
                type="text"
                class="form-control"
                (input)="onUpdateServerName($event)">
            <p>{{serverName}}</p>

        and on the .ts file define the method:
            serverName = ' ';
            onUpdateServerName(event: Event) {
                //console.log(event);
                this.serverName = (<HTMLInputElement>event.target).value;
            }


- Two Way Binding
    is similar to event binding but it actually acts both ways on the element/variable,
    which makes things simpler.
    looking at the example above, this is how it looks with two way binding:

        define the HTML:
            <input
                type="text"
                class="form-control"
                [(ngModel)]="serverName">
            <p>{{serverName}}</p>

        and on the .ts file we don't need the method:
            serverName = ' ';

    with two way binding, if you update the input value, the value stored by 
    serverName will change with it but also if you change the serverName value the 
    value of the input in the HTML code will also change which is a very useful feature.
    "ngModel" is an Angular special tag and for this functionality to be avilable the 
    FormsModule needs to be added to the app.module file. don't forget to add the 
    import { FormsModule } from '@angular/forms' statement.

----------------------------------------------------------------------------------------------

                            Predefined Directives

Directives are Instructions in the DOM

- ngIf
    it's a structural directive as it adds or removes an element hence it changes the s
    structure of the DOM 
    example of usage:
        <p *ngIf="serverCreated">Server was created, server name is {{ serverName }}</p>
    
    note the *, this is because ngIf will actually alter the structure of the DOM.

- ngIf with else
    an interesting addition to ngIf is two use it with else:
        <p *ngIf="serverCreated; else noServer">Server was created, server name is {{ serverName }}</p>
        <ng-template #noServer>
        <p>No Server created!</p>
        </ng-template> 

    the #noServer is like a place holder
    this is like a if else statement really.

- ngStyle





            
         








    

 
















