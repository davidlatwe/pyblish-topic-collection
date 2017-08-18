Source : [The use of hosts attribute?](http://forums.pyblish.com/t/the-use-of-hosts-attribute/78)

Time : May 17, 2015


## Not having the host attribute would be easier ?

* case 1: host specific plugin

    Basically when having a host specific plugin, one would import the hosts api at the top of the plugin, resulting in that plugin not being included cause the import fails on other hosts.

    So in theory I wouldn't need to specify a host in this case.

* case 2: multi-host compatible plugin

    There is the case of plugins that are multi-host compatible, and uses only python libraries.
    In this case I would assume the plugins not to be selectors, and therefore reliant on instances to execute, meaning that in the hosts the plugin isn't compatible with the instances wouldn't be present.


## It may seem unnecessary, but...

The `hosts` attribute is one of the optional ways you can associate a registered plug-in with data, similar to `families`.
One distinguishes between the environment (`host`) and the other between content (`families`).

###### for organizing
Whether you need to make the distinction in your collection of plug-ins depends on how your write and organize them.

You can, for example, register plug-ins only relevant to a particular host, in which case a plug-in of an unsupported host may never be registered in the first place and thus not be affected by the filtering mechanism.

But if you do register one plug-in with support for one host, and one with support for another, then the hosts attribute can help you distinguish between which plug-in operates in which host.

###### for communication

Consider still making note of which hosts and families are supported via the corresponding attributes for the purpose of communication.

In a lengthy plug-in, it might get difficult for another developer, or your future self, to figure out which hosts a plug-in supports, especially when a host-library isn't being directly imported at the top of the file or when said library isn't one we recognise (like one from Clarisse or Cinema4D).

###### it's optional
I think with the [new defaults](http://forums.pyblish.com/t/api-changes/51/3?u=marcus) for `hosts` and `families` this will make more sense as being optional.
If you can't find a need for them right away, don't fret. And if the time comes when you do need to make this distinction, you can.

## Future

There are a few other ways planned for future releases.
* Filter by version
* Filter by OS

```python
class ValidateInstance(...):
   families = ["myFamily", "myFamily.childA"]
   hosts = ["hostA", "hostB"]
   version = "2.4.1"
   oss = ["win", "osx"]
```
And like with `hosts` and `families`, depending on the complexity and size of your plug-in collection, and how you organize them, all or none of these may be necessary.

###### at least filling them out as a habit

You may be looking for a Maya plug-in, or a plug-in related to OSX file permissions or a later version of a plug-in you already have. These attributes make this possible and I would make it a habit of at least filling them out, if not only for the purpose of future-proofing them.