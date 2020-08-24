



# Commands

> manage.py help

> python manage.py migrate

> python manage.py runserver
> 

Make migrations:

> python manage.py makemigrations


Showing the sql queries to create those models. 0001 is the control version id that was created when makemigrations

> python manage.py sqlmigrate GestionPedidos 0001


# Notes

Python uses sqlite3 database by default.


Each function in views.py is a view.

Django is url friendly. This format is recommended: root/date/2017 instead of using ?date=2017


# Template


You can import Template and Context from Django and create html templates in a file using variables like {{etc}}, pass a dictionary to the Context and call render on the tpl and Django will take care of it.

```python

plt = Template(html_string)

ctx = Context({"name", "Jeremy", "date", date_obj, "numbers": [1, 2, 3, 4]})

my_template = plt.render(ctx)


### Or


### In .html

"""

    {{name}}
    {{date_obj.now()}}

    {% for i in numbers %}
        <p1>{i}</p1>
    {% endfor %}

    {% if %}

    {% else %}

    {% endif %}



"""

def get_template(request):
    my_template = loader.get_template("MyTemplate.html")
    rendered = my_template.render({"name": "Jeremy"})
    return HttpResponse(rendered)

```

You can also include other templates in a template like {% include "other-template.html" %}


# Apps

When you create an app in a project, add it to settings INSTALLED_APPS. You can run pythong manage.py check YourProject



