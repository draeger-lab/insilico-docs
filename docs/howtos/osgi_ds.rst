=========================
OSGi Declarative Services
=========================

Declare Service (or DS for short) is the OSGi way to request or provide
implementations across bundles.

Enable DS Annotations Support in Eclipse
========================================

1. Open :code:`Preferences...`
2. Select :code:`Plug-in Development > DS Annotations`
3. Check :code:`Generate descriptors from annotated sources`
4. (Optional) Enter :code:`OSGI-INF/services` in the textfield :code:`Descriptor directory` to follow the InSilico conventions.
5. Check :code: `Add DS Annotations to classpath`
6. Check :code:`Generate header "Bundle-ActivationPolicy: lazy"`


Provide a Service Interface
===========================

To mark a class as a service provider mark it with the :code:`@Component` annotation.
This will trigger the auto-generation of a component definition file when ever
the java file is saved.

The generated component definition provides support for every interface which is
implemented by the annotated class. If the component should provide the interface
which is implemented in a parent class, you have to redeclare the conformance in
the annotated class in order to generate a correct component definition.

Consume a Service
=================

TODO
