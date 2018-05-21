=======================
How To Add A New Editor
=======================

Usefull Services
================

The :code:`EditorOpener` should be obtained by dependency injection. By default
the :code:`ProxyEditorOpener` will be injected. This implementation will lookup the
service registry for other :code:`EditorOpener` and try to call the top most component.
If this fails or no editor is aviable the :code:`DefaulEditorOpener` will be used.

The :code:`DefaulEditorOpener` will search for an already open editor part in the model.
If none is found it will create a new part and ask the first
:code:`EditorClassURLProvider` to provide a bundle class URI for this part. Also the
first :code:`FileIconProvider` will be asked to provide a matching icon for this
part. After creating the part, the editor will be activated.


FileIconProvider
----------------
Bundle: org.eclipse.fx.code.editor
Class: org.eclipse.fx.code.editor.services.FileIconProvider

Get the URI to a document and return a URI for an icon which should be used for
this type of files.


EditorOpener
------------
Bundle: org.eclipse.fx.code.editor
Class: org.eclipse.fx.code.editor.services.EditorOpener

With the :code:`public boolean test(String uri);` method you can check if you could
open a editor for the given :code:`URI`. If you return :code:`true` the
:code:`public boolean openEditor(String uri);` method will be called. After this call
the editor should be added to the application model.

There are two default implementations in efxclipse: :code:`DefaulEditorOpener`and
:code:`ProxyEditorOpener`.

EditorOpenerTypeProvider
------------------------
Bundle: org.eclipse.fx.code.editor
Class: org.eclipse.fx.code.editor.services.EditorOpenerTypeProvider

A :code:`EditorOpenerTypeProvider` will be asked which :code:`EditorOpener` should be used
to open a editor for a given URI (as String).

EditorClassURLProvider
----------------------
Bundle: org.eclipse.fx.code.editor.fx.e4
Class: org.eclipse.fx.code.editor.fx.e4.EditorClassURLProvider


Get the URI to a Document and return a Bundle-Class for an Editor which could
handle the given file type. This service component is only be called when the
:code:`DefaulEditorOpener` is used.

Example
=======
TODO
