#Metodyka a metodologia 

Jak tłumaczy Uniwersalny Słownik Pojęć Języka Polskiego, metodyka: 
1.	zbiór zasad dotyczących sposobów wykonywania jakiejś pracy lub trybu postępowania prowadzącego do określonego celu. 
2.	w pedagogice: dydaktyka szczegółowa jakiegoś przedmiotu szkolnego, omawiająca cele i sposoby nauczania tego przedmiotu

metodologia zaś: 

Nauka o metodach badań naukowych i o sposobach przeprowadzania analiz oraz oceniania wartości poznawczej poszczególnych dyscyplin naukowych.
Najprościej jednak charakteryzuje to Wielki Słownik Poprawnej Polszczyzny , gdzie metoda to po prostu „sposób robienia czegoś” natomiast metodologia to „nauka o metodach badań naukowych, o skutecznych sposobach dociekania ich wartości poznawczej”. 


#Kanban
* http://en.wikipedia.org/wiki/Kanban_(development)
* https://www.crisp.se/file-uploads/Kanban-vs-Scrum.pdf
* http://www.everydaykanban.com/what-is-kanban/
* http://dailyweb.pl/wirtualna-tablica-kanban-konkurs/
* http://kanbantool.com/pl/

#MVC Active and Passive model

![Passive](https://i-msdn.sec.s-msft.com/dynimg/IC108622.gif) 

W modelu pasywnym, kontroler informuje widok o zmianie modelu.

![Active] (https://i-msdn.sec.s-msft.com/dynimg/IC100217.gif)

W modelu aktywnym to model informuje widok, kiedy Model jest zmieniony przez kontroler. 


#Routing poprzez atrybuty

W MVC wersji 5 zostal wprowadzony nowy system routingu definiowany poprzez atrybuty (Route, RoutePrefix, etc). Routing aktywuje się poprzez wywolanie metody *'MapMvcAttributeRoutes'* z klasy *RouteCollection* przy rejestracji scieżek.

   ```C#
   routes.MapRoute(
    name: "ProductPage",
    url: "{productId}/{productTitle}",
    defaults: new { controller = "Products", action = "Show" },
    constraints: new { productId = "\\d+" }
    );
   ````
   

   * Wartości domyślne
   ```C#
   [Route("books/lang/{lang=en}")]
    public ActionResult ViewByLanguage(string lang)
    {
        return View("OneBook", GetBooksByLanguage(lang));
    }
    ```
    
   * Routing z prefixem
   ```C#
   public class ReviewsController : Controller
{
    // eg: /reviews
    [Route("reviews")]
    public ActionResult Index() { ... }
    // eg: /reviews/5
    [Route("reviews/{reviewId}")]
    public ActionResult Show(int reviewId) { ... }
    // eg: /reviews/5/edit
    [Route("reviews/{reviewId}/edit")]
    public ActionResult Edit(int reviewId) { ... }
}
````

* Ścieżka domyślna
```C#
[RoutePrefix("promotions")]
[Route("{action=index}")]
public class ReviewsController : Controller
{
    // eg.: /promotions
    public ActionResult Index() { ... }
 
    // eg.: /promotions/archive
    public ActionResult Archive() { ... }
 
    // eg.: /promotions/new
    public ActionResult New() { ... }
 
    // eg.: /promotions/edit/5
    [Route("edit/{promoId:int}")]
    public ActionResult Edit(int promoId) { ... }
}
```

##Ograniczenia


* {x:alpha}
* {x:bool}
* {x:datetime}
* {x:decimal}
* {x:double}
* {x:float}
* {x:guid}
* {x:int}
* {x:length(6)} 
* {x:length(1,20)}
* {x:long}
* {x:max(10)}
* {x:maxlength(10)}
* {x:min(10)}
* {x:minlength(10)}
* {x:range(10,50)}
* {x:regex(^\d{3}-\d{3}-\d{4}$)}

  *Przykładowe ograniczenie*
  ```C#
   [Route("users/{id:int:min(1)}")]
   public ActionResult GetUserById(int id) { ... }
  ```
