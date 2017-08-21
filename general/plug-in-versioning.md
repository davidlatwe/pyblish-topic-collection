Source : [Plug-in versioning](http://forums.pyblish.com/t/plug-in-versioning/23)
Original from [Google Group](https://groups.google.com/forum/m/#!topic/pyblish/qCgYvlIi3WE)

Time : Apr 30, 2015
Original Time : Aug 29, 2014


## Versioning

[issue #118](https://github.com/pyblish/pyblish-base/issues/118)

When we make a change to the backend (Pyblish-base API), all plugins could potentially stop working, because they no longer match the interface provided by their superclass.

This should be okay, but at the moment there isn’t any way for such events to fail gracefully.

Adding a `requires` attribute, next to `families` and `version` in the superclass for plugins for them to specify with which version of Pyblish they are compatible with.

```python
# superclass
class Plugin():
    hosts = ["*"]
    families = ["*"]
    order = -1
    requires = "pyblish>=1"
```

See here for an example implementation in Rez.

* http://nerdvegas.github.io/rez/#versioning


```
===========   =================================================
Requirement   Description
===========   =================================================
foo           any version of foo
foo>=5        any version of foo, above or equal to 5
foo>=5.6      any version of foo, above or equal to 5.6
foo==5.6.1    exact match
foo>5         foo-5 or greater, including minor and patch
foo>5, <5.7   foo-5 or greater, but less than foo-5.7
foo>0, <5.7   any foo version less than foo-5.7
===========   =================================================
```