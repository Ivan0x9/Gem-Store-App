> app.js
    (function() {
        var app = module('ExampleApp', ['simple-directives']);
            // simple-directives je naziv nekog drugog custom modula koji ti napraviš.
            // Dakle, array prima module kao što su o ovom slučaju 'simple-directives'.
        
        app.controller('ImeKontrolera', function() {
            // do something;
        });
    })();
=========================================================================================================
> neki.js
    (function() {
        var app = module('simple-directives', []); // sad je napravljen custom module koji nema dependecije drugih modula
        app.directive('nekaDirektiva', function() {
            return {
                restrict: 'E', // E je za html Element, može i A za atribut html elementu. Postoje još C, EA, itd.
                               // (Attribute) A =  <div Doc></div>
                               // (Class) C =  <div class="Doc"></div>
                               // (Element) E =  <Doc data="book_data"></Doc>
                               // (coMment) M =  <!--directive:Doc -->
                               // Drugim riječima, kažeš ovoj direktivi kako se mora ponašat unutar html-a stranice, odnosno kako će ih angular interpretirat.
                templateUrl: 'neki-page.html', // template se u ovom slučaju nalazi u istom folderu di je neki.js pa ne treba kopat po hijerarhiji
                controller: function() {
                    // do something
                    // Evo, sad je controller unutar direktive. To znači da ga ne treba u html-u pozivat s ng-controller.
                },
                controllerAs: 'neki' // sad se ovdje može imenovat kao šta se moglo u ng-controller sa "as neki"
            };
        });
    })();
=========================================================================================================
> index.html
    <html ng-app="ExampleApp">
        // . . .
        <body ng-controller="ImeKontrolera as kontroler"> // s obzirom da je ovo kontroler iz app.js onda ga treba navest s ng-controller
            <div ng-repeat="item in kontroler.item">
                <h3>{{item.name}}</h3>
                <p>{{item.price}}</p>
            </div>
            // . . .
            <neki-page></neki-page>
            // sad će s ovim angular prepoznat direktivu i vodit do html-a koji je naveden te će se load-at s kontrolerom svojim
        </body>
    </html>
=========================================================================================================
> neki-page.html
    // ne mora imat html, head, body tagove jer će se ionako nalazit na index.html ti tagovi. Manje kodiranja. <3
    <h4>Description</h4>
    <blockquote>{{item.description}}</blockquote>
