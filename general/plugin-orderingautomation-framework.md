Source : [Plugin Ordering/Automation Framework](http://forums.pyblish.com/t/plugin-ordering-automation-framework/45)
Original from [Google Group](https://groups.google.com/forum/#!topic/pyblish/NQCOKmI0xW4)


Time : May 2, 2015
Original Time : Sep 14, 2014


Pyblish-base version during that time : [1.0.15](https://github.com/pyblish/pyblish-base/releases/tag/1.0.15)

## Plugin Ordering

The ordering in which plugins are currently being run.

`Selection -> Validation -> Extraction -> Conform`

> Editor:
> The terms of the publish workflow has been changed to
> `Collection -> Validation -> Extraction -> Integration`

Example:
```python
class SelectObjectSet(Selector):
    order = 0

class ValidateNamingConvention(Validator):
    order = 1

class ExtractAsMa(Extractor):
    order = 2

class ConformWithAsana(Conform):
    order = 3
```

The order attribute located on each plugin.
All we have to do is query this number upon running a publish.

```python
plugins = discover()
plugins_in_order = sorted(plugins, key=lambda p: p.order)
```
Viola !
```python
for plugin in plugins_in_order:
     plugin().process(context)
```
