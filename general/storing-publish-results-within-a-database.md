Source : [Storing publish results within a database](http://forums.pyblish.com/t/storing-publish-results-within-a-database/47)

Time : May 3, 2015


## Store the results of the Publishing process into a database

Discussions about the best way of getting this accomplished.
And about the different pros and cons that this approach might have.

###### Information to be stored

* Name of the asset being published
* Name of the artist Publishing the asset
* Date of the Publish
* Project that the asset belongs to
* *Information of the results of each plugin*
* ...

###### First things first

Define the following things:
* Structure of the database (Schema)
* The best way to retrieve information from plugins in preparation for the database


---

###### SQL vs. JSON

Don't go for SQL, go for a JSON-based database, like MongoDB (local) or Firebase (cloud).

SQL is restrictive whereas JSON is loose.

Practically, JSON will make your journey towards understanding what data you actually need and how you intend on using it a lot smoother than anything involving SQL.

For example, a JSON-based database can be exported/imported as plain JSON without loss of data. 

It's also good for embedding directly in Instances and the Context, as it's just a dictionary in Python-land. Tables offer nothing like that.

###### Information of the results of each plugin

The manner in Pyblish processing instances, works in the form of **pairs**.

A pair is simply an Instance/Plug-in combination.
After a completed publish, the processing history looks something like this.

```
SelectInstances:           Context;
ValidateNamespaces:        InstanceA;
ValidateNamespaces:        InstanceB;
ValidateSomethingAboutA:   InstanceA;
ExtractInstances:          InstanceA;
ExtractInstances:          InstanceB;
...
```

In addition of gathering all information about a particular plug-in, you'll also need to take into account each instance it processed. The result could look something like:

```json
[
  {
    "plugin": "ValidateSometing",
    "instance": "InstanceA",
    "success": true
  },
  {
    "plugin": "ValidateSometingElse",
    "instance": "InstanceA",
    "success": false
  } 
]
```

###### Getting crackin'

* **Structure of the database (Schema)**

  If you go for JSON, you can work this out as you go. You can start throwing data into your database, and make use of it. As soon as you find something missing, you add it.


* **The best way to retrieve information from plugins in preparation for the database**

  All log messages and exceptions will be available via the `context.data("results")` member. In addition to that, you could append information in each plug-in where it makes sense.

  ```python
# ValidateNamespaces
if error:
   data = context.data("toDatabase", list())
   data.append({
      "plugin": type(self).__name__,
      "message": "Custom message, just for the database, not for the user or GUI"
   }
   context.set_data("toDatabase", data)
```

  In this case, a particular plug-in attaches information that is specifically meant for a database, something that won't be logged or raised.

  Every plug-in could have this, and each plug-in will have intimate knowledge about what it's doing, which makes it a good spot to generate this data from.


###### Notes

A JSON-based database is identical to working with a JSON on disk, so I would start by writing to a JSON as in the plug-in you posted, and transition to the database when you need higher performance. JSON on disk should be very capable of storing thousands if not millions of records without any noticeable drop in performance, but querying is another question, unless you know what you're looking for.

---

## Start using the data for statistics

###### Do you have any particular tool in mind for visualization?

* **Elasticsearch & Kibana**

  https://www.elastic.co/products/kibana
  
  http://logstash.net/docs/1.4.2/learn
  
  "ELK stack", for Elasticsearch, Logstash and Kibana

* **PyGal**
  
  http://pygal.org/en/stable/
  
  Can exports to SVG
  
* **D3.js**
  
  visualisation through a web browser
  
  need some basic familiarity with JavaScript






