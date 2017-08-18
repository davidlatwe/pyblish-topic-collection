Source : [Selection ID](http://forums.pyblish.com/t/selection-id/32)
Original from [Google Group](https://groups.google.com/forum/#!topic/pyblish/rNS7TFAHRtY)


Time : May 2, 2015
Original Time : Sep 28, 2014


## Using ID for instances to match Instance and Selector

> Editor:
> Notice, "Selector" is an old term, it's "Collector" now.

Using an **ID** for instances to match Instance and Selector, much like we are with **Family** and **Plugin**.

###### The Problem

In Maya, to tag a node in our scene with an attribute.

```json
{
  "publishable": true,
  "family": "demo.model"
}
```

The existence of these two attributes, along with the node having a type of “objSet”, would make Pyblish identify the node as being an instance.

But these two attributes are so generic, if we were to make a new selector and no longer wanted to use any other, we would have had to make up some other attributes so as to not have our instance get picked up by both selectors. E.g.

```json

{
  "myCustomIdentifier": true,
}
```

Ultimately ending up with lots of identifiers without any relation.

---

###### The Solution

The ID, on the other hand, would allow for an arbitrary amount of selectors, whilst still keeping them somewhat related by them all having an identical key, namely id, and variable value, such as `pyblish.instance`

An independent provider of Selectors could then occupy their own range of IDs, without risking to pick up the wrong instances from a scene.

```json

{
   "id": "pyblish.instance"
}
```

If I’m working on an extension ([napoleon](https://github.com/pyblish/pyblish-napoleon)) for Pyblish with additional Selectors, I could use something like:

```json
{
   "id": "pyblish.napoleon.instance"
}
```
This way, the Napoleon selectors could remain discoverable ( *discover by `pyblish.api.discover()`*) but never accidentally pick up an instance that wasn’t intended for the Napoleon selectors.

And the same goes for anyone’s custom selectors. We could have any number of selectors, all active at the same time, and tag our instances however we please and have an appropriate selector come pick it up.

###### Customisable

The value of id may be configurable via the pyblish user-configuration.

```json
identifier: "myId"
```

Napoleon selector Example code:
( example code down below is modified from [here](https://github.com/pyblish/pyblish-napoleon/blob/master/napoleon/plugins/collect_napoleon_instances.py) to match current pyblish-base version )

```python
import pyblish.api

class CollectNapoleonInstances(pyblish.api.ContextPlugin):
	hosts = ['maya']
	label = 'Select via Object Set'

	def process(self, context):
		import maya.cmds as cmds
		
		for objset in cmds.ls("*.id",
							  objectsOnly=True,
							  type='objectSet',
							  long=True,
							  recursive=True):  # Include namespace

			if not self.is_instance(objset):
				continue

			# do something about it...


	def is_instance(self, node):
		identification = cmds.getAttr(node + ".id")
		if identification.startswith('pyblish.napoleon.instance'):
			return True
		return False

```

