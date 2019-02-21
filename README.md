# ASP.NET MVC: How to set CSS class  active in menu item

Please perform the following steps to implement active class  in your menu
## Create a class named ```utility``` as following

```
public class Utility
    {
        public static string ActiveSelector(string controller, string action = "", string parameters = "")
        {
            var queryString = HttpContext.Current.Request.QueryString;
            var currentRouteData = HttpContext.Current.Request.RequestContext.RouteData;
            string returnval = "";
            returnval = currentRouteData.Values["controller"].ToString().ToLower() == controller.ToLower() &&
                (string.IsNullOrEmpty(action) || currentRouteData.Values["action"].ToString().ToLower() == action) &&
                (string.IsNullOrEmpty(parameters) || string.IsNullOrEmpty(queryString[parameters.Split('=')[0]]) || queryString[parameters.Split('=')[0]].ToLower() == parameters.Split('=')[1]) ? "active" : "";
            return returnval;
        }
    }

```



Now, use above static method to generate menu in your view as following. Note: set your controller name in ```controller```, 
method or action name in ```action``` and if you want to make active for certain route values then pass route in query string format into ```queryString```. Here, action or method and query string is optional
```html
<li class="@Utility.ActiveSelector("controller", "action", "querystring")"></li>
<li class="@Utility.ActiveSelector("student", "details", "studentId=1")"></li>
<li class="@Utility.ActiveSelector("student", "studentList")"></li>
```
##If you want to generate active class where ```url``` contains ```controllerName``` then perform following :

```html
<li class="@Utility.ActiveSelector("student")"></li>
```
In this way you can set active class to menu link dynamically.
