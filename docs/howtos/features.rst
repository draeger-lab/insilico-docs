========
Features
========

Create A New Feature
====================

1. Select :code:`File > New > Project..`
2. Select :code:`Plug-in Development > Feature Project`
3. Enter a name for the feature project
   - The name should match the symbolic name of the feature
4. Uncheck :code:`Use default location`
5. Enter the location for the project
   - The plugin project should be located in :code:`insilico/features`
   - The name of the folder should match the symbolic name of the feature
6. Select :code:`Next`
7. Select the plugins which should be contained in this feature
8. Select `Finish`

Because InSilico uses Maven Tycho to build the final product we have to convert
our feature project into a Maven project:

1. Right click on the feature project
2. Select :code:`File > New > File`
3. Enter :code:`pom.xml` as file name
   - Ensure that the root folder of the feature project is selected as location
4. Select :code:`Finish`
5. Open :code:`pom.xml`
6. Copy and paste the template from below

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
  <project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
  xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <modelVersion>4.0.0</modelVersion>

    <parent>
      <groupId>org.draegerlab.insilico</groupId>
      <artifactId>org.draegerlab.insilico.features</artifactId>
      <version>1.0.0-SNAPSHOT</version>
      <relativePath>../</relativePath>
    </parent>

    <!-- Insert symbolic name of your feature -->
    <artifactId>XYZ</artifactId>
    <packaging>eclipse-feature</packaging>
  </project>



TODO add pom
TODO add to feature project
