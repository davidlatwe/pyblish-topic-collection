Source : [Timestamp standard](http://forums.pyblish.com/t/timestamp-standard/80)


Time : May 19, 2015


## Standardize how time is represented throughout Pyblish

[RFC3339](https://tools.ietf.org/html/rfc3339), which defines [ISO 86011](https://en.wikipedia.org/wiki/ISO_8601) like this.
```
2015-05-18T07:27:40.6766Z
```
Where **T** can be thought of as a space-character, and **Z** denotes that it is relative UTC, which is 1 hour behind of GMT.

It will be used for visualising time taken:

* Per publish
* Per plug-in
* Per function within plug-in

> some become presenting as "duration"

For the purposes of:

* Debugging
* Archiving
* Auditing

```python
import pyblish.lib
pyblish.lib.time()
```