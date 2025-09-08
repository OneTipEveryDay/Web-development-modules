# What does Django code look like?
> In a traditional data-driven website, a web application waits for HTTP requests from the web browser (or other client). When a request is received the application works out what is needed based on the URL and possibly information in POST data or GET data. Depending on what is required it may then read or write information from a database or perform other tasks required to satisfy the request. The application will then return a response to the web browser, often dynamically creating an HTML page for the browser to display by inserting the retrieved data into placeholders in an HTML template.
>
> <img width="1125" height="769" alt="image" src="https://github.com/user-attachments/assets/efc57795-6053-45e3-903d-02edb87962ac" />

> URLs: While it is possible to process requests from every single URL via a single function, it is much more maintainable to write a separate view function to handle each resource. A URL mapper is used to redirect HTTP requests to the appropriate view based on the request URL. The URL mapper can also match particular patterns of strings or digits that appear in a URL and pass these to a view function as data.
>View: A view is a request handler function, which receives HTTP requests and returns HTTP responses. Views access the data needed to satisfy requests via models, and delegate the formatting of the response to templates.
>Models: Models are Python objects that define the structure of an application's data, and provide mechanisms to manage (add, modify, delete) and query records in the database.
>Templates: A template is a text file defining the structure or layout of a file (such as an HTML page), with placeholders used to represent actual content. A view can dynamically create an HTML page using an HTML template, populating it with data from a model. A template can be used to define the structure of any type of file; it doesn't have to be HTML!

 ## Sending the request to the right view (urls.py)
> A URL mapper is typically stored in a file named urls.py. In the example below, the mapper (urlpatterns) defines a list of mappings between routes (specific URL patterns) and corresponding view functions. If an HTTP Request is received that has a URL matching a specified pattern, then the associated view function will be called and passed the request.
>
```py
 urlpatterns = [
    path('admin/', admin.site.urls),
    path('book/<int:id>/', views.book_detail, name='book_detail'),
    path('catalog/', include('catalog.urls')),
    re_path(r'^([0-9]+)/$', views.best),
]
```

The urlpatterns object is a list of path() and/or re_path() functions (Python lists are defined using square brackets, where items are separated by commas and may have an optional trailing comma. For example: [item1, item2, item3,]).


 ## Handling the request (views.py)
> Views are the heart of the web application, receiving HTTP requests from web clients and returning HTTP responses. In between, they marshal the other resources of the framework to access databases, render templates, etc.
>
```py
 # filename: views.py (Django view functions)

from django.http import HttpResponse

def index(request):
    # Get an HttpRequest - the request parameter
    # perform operations using information from the request.
    # Return HttpResponse
    return HttpResponse('Hello from Django!')
  ```

Views are usually stored in a file called views.py.



## Defining data models (models.py)

> Django web applications manage and query data through Python objects referred to as models. Models define the structure of stored data, including the field types and possibly also their maximum size, default values, selection list options, help text for documentation, label text for forms, etc. The definition of the model is independent of the underlying database
> The code snippet below shows a very simple Django model for a Team object. The Team class is derived from the Django class models.Model. It defines the team name and team level as character fields and specifies a maximum number of characters to be stored for each record. The team_level can be one of several values, so we define it as a choice field and provide a mapping between choices to be displayed and data to be stored, along with a default value.
>
> ```py
> # filename: models.py

from django.db import models

class Team(models.Model):
    team_name = models.CharField(max_length=40)

    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11', 'Under 11s'),
        # …
        # list other team levels
    )
    team_level = models.CharField(max_length=3, choices=TEAM_LEVELS, default='U11')
    ```

   ## Querying data (views.py)

   > The code snippet shows a view function (resource handler) for displaying all of our U09 teams. The list_teams = Team.objects.filter(team_level__exact="U09") line shows how we can use the model query API to filter for all records where the team_level field has exactly the text U09 (note how this criteria is passed to the filter() function as an argument, with the field name and match type separated by a double underscore: team_level__exact).
> 
```py
## filename: views.py

from django.shortcuts import render
from .models import Team

def index(request):
    list_teams = Team.objects.filter(team_level__exact="U09")
    context = {'youngest_teams': list_teams}
    return render(request, '/best/index.html', context)
```
> This function uses the render() function to create the HttpResponse that is sent back to the browser. This function is a shortcut; it creates an HTML file by combining a specified HTML template and some data to insert in the template (provided in the variable named context). In the next section we show how the template has the data inserted in it to create the HTML.
>
> ## Rendering data (HTML templates)
>
> Template systems allow you to specify the structure of an output document, using placeholders for data that will be filled in when a page is generated. Templates are often used to create HTML, but can also create other types of document. Django supports both its native templating system and another popular Python library called Jinja2 out of the box (it can also be made to support other systems if needed).
> The code snippet shows what the HTML template called by the render() function in the previous section might look like. This template has been written under the assumption that it will have access to a list variable called youngest_teams when it is rendered (this is contained in the context variable inside the render() function above). Inside the HTML skeleton we have an expression that first checks if the youngest_teams variable exists, and then iterates it in a for loop. On each iteration the template displays each team's team_name value in an <li> element.


## filename: best/templates/best/index.html

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Home page</title>
</head>
<body>
  {% if youngest_teams %}
    <ul>
      {% for team in youngest_teams %}
        <li>{{ team.team_name }}</li>
      {% endfor %}
    </ul>
  {% else %}
    <p>No teams are available.</p>
  {% endif %}
</body>
</html>
```


















