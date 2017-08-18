Source : [Background Publishing](http://forums.pyblish.com/t/background-publishing/85)


Time : May 25, 2015


## Background Publishing

[issue #89](https://github.com/pyblish/pyblish-base/issues/89)

Background Publishing is about running a publish in the background so that users can continue working.

---

What if, whenever you hit Publish:

* Your scene is saved (into a temp-dir that you cannot see nor touch)
* Launches Pyblish standalone
* Publish then run solely on the saved file, without interaction with current opened file

###### Benefits

* support for any host, even those without scripting capabilities nor integration.

    In worst case, asking the user to open it themselves once the scene has been saved into the designated location.
    For example, an artist could save out JPEGs from Photoshop or sculptures from ZBrush and validate those before conforming them to an asset library.
    
* publishing without interfering with the scene.

    A user can publish, it can take however long it takes, and move on with his work undisturbed.

* publishing can be destructive.
    
    That publishing could make permanent changes to the scene before performing any serialisation.
    For example, it may be desired to bake all keys so as to not bring along any constraints or expressions. As baking alters the scene, this can be difficult and error-prone in the currently opened scene.

###### Disadvantages

* unable to interact with your scene through Pyblish, such as performing repairs or custom actions.

###### Related

[Command-line Publishing](http://forums.pyblish.com/t/commandline-publishing/69/3)

---

#### Thoughts about doing Background Publishing

Have to make sure that the newly spawned instances have identical environment to the original.
At least the environment variables should remain identical, or can be made identical fairly easy.


Useful when extracting data that takes a long time.
Although I do find when artists wants to publish, it is to get feedback or think they are done. 
In both cases they wouldn't go back to the work file, so if the extraction failed they would have reopen the file.

---

[Some new ideas](https://github.com/pyblish/pyblish-base/issues/89#issuecomment-311009033) for this.
* Collection and validation runs locally
* Extraction and integration runs remotely


