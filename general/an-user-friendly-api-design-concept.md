Source : [An User friendly API design concept](http://forums.pyblish.com/t/an-user-friendly-api-design-concept/24)
Original from [Google Group](https://groups.google.com/forum/#!topic/pyblish/qKOgizaICQ4)

Time : Apr 30, 2015
Original Time : Sep 28, 2014

## How to create an user friendly API.

We may use one or more API for a single task.
How to create an user friendly API.

If you have good documentation for this API , your problem got solved.
But for someone who wanna try different API for the same time he may not have good time to read all the docs.
If the API is not a straight forward one then we have to quit trying it or look for some assistance.

At least we can standardize some part of it, for eg: `read` and `write`. (**method classifications**)

example:
```python
from database import db

class MyAPI(object):
def __init__(self):
self.person = Person()

class Person(object):
def __init__(self):
self.db = db()
self.db.register_user(username="liju.kunnummal")
self.read = PersonRead(self.db)
self.write = PersonWrite(self.db)

class PersonRead(object):
def __init__(self, db):
self.db = db

def all_shows(self):
return self.db.get_user_shows()

def user_data(self):
return self.db.get_user_data()

class PersonWrite(object):
def __init__(self, db):
self.db = db

def current_show(self, show_name):
self.db.set_user_current_show(show_name)

def current_task(self, current_task):
self.db.set_current_task(current_task)
```

How do we use this?

```
>>> api = MyAPI()
>>> api.person.read.allShows()
>>> api.person.read.user_data()
>>> api.person.write.current_show("SHOW02")
>>> api.person.write.current_task(taskObj)
```

When we type `api.person.___` we will think about what we wanna do.
For reading something, go `api.person.read.____`
For setting something, than `api.person.write.____`

This will reduce the ambiguity while using methods.

---
###### What if other than read/write ?

We can still use the same idea by **classifying methods**.
Example, `execute something`.

```python
class Person(object):
def __init__(self):
self.db = db()
self.db.register_user(username="liju.kunnummal")
self.read = PersonRead(self.db)
self.write = PersonWrite(self.db)
self.process = PersonProcess(self.db)
```

We can add all execution methods to `PersonProcess` class, and use

```
>>> api.person.process.used_data()
>>> api.person.process.all_task()
```

This applicable to all instance we have in our API, which avoids confusion among methods while using them and gives you an user friendly API.



