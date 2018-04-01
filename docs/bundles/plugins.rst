=======
Plugins
=======

A Plugin is a OSGi Bundle with a additional `plugin.xml` file.

Dependencies
============

Declare your dependencies in the :code:`MANIFEST.MF` file. You should use the
Eclipse Editor for this.

Extensions
==========

You can declare extensions to an existing extension point via the :code:`plugin.xml` file.
That's also where you expose your own extension points.
It's recommended to use the Eclipse Editor for this task.
