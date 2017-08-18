Source : [Integrations and Extensions](http://forums.pyblish.com/t/integrations-and-extensions/33)
Original from [Google Group](https://groups.google.com/forum/#!topic/pyblish/LOC6zFPV9t0)


Time : May 2, 2015
Original Time : Sep 14, 2014

## Make a separation between integration and extension


###### Overview

**Pyblish for Maya** integrates Maya with Pyblish via the file-menu item.
Eventually, it will also provide the implementation that communicates with the GUI.

It also provides a few plug-ins. These plugins extend Pyblish in a way specific to Maya.

If we refer to the menu-item and GUI integration stay as an **integration** of Pyblish, we could refer to the plugins themselves as an **extension**.

---
###### The future

Like there to be plenty of extensions, but only a few integrations.

An extension could potentially utilize an integration, become dependent on it.

As an extension to Pyblish that utilize the Maya integration.

This could be a workflow extension, with conventions implemented from a particular user or studio. The workflow can then be documented and contributed to like any other project on GitHub. This way we can expose workflows typically only available from within an organisation.

* pyblish-ilm-rigging
* pyblish-blur-modeling
* pyblish-spiderman

It can more easily be perfected, documented and used.

`pip` provides a features that allows us to create dependencies between packages.

For example, installing the `pyblish-ilm-rigging` could automatically install `pyblish` and `pyblish-maya` if it turns out that it was dependent on those. This way, users won’t be bothered with details and can just install whichever extension they would like to try out.