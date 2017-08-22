Source : [SimplePlugin](http://forums.pyblish.com/t/simpleplugin/60)

Time : May 6, 2015


## To provide for arbitrary plug-ins that does anything

released in [1.1.0](https://github.com/pyblish/pyblish-base/releases/tag/1.1.0)

issue [#186](https://github.com/pyblish/pyblish-base/issues/186)



Plug-ins are typically intended for a particular purpose, such as validating or extracting.
But simple plug-ins doesn't have a particular purpose.

> Simple Plugin is ContextPlugin and InstancePlugin's superclass.
> Give possibility to go outside of the framework of CVEI.

```python
import pyblish.api

class MyPlugin(pyblish.api.Plugin):
  order = -1
  def process(self):
    self.log.info("I'm simple")
```