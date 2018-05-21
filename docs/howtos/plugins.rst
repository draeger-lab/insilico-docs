=======
Plugins
=======

This section contains useful informations about creating and mainting plugin projects.

Create A New Plugin
===================

1. Select :code:`File > New > Project..`
2. Select :code:`Plug-in Development > Plug-in Project`
3. Enter a name for the plugin project
   - The name should match the symbolic name of the plugin
4. Uncheck :code:`Use default location`
5. Enter the location for the project
   - The plugin project should be located in :code:`insilico/bundles`
   - The name of the folder should match the symbolic name of the plugin
6. Select :code:`Next`
7. (Optional) Check :code:`Generate an activator` if you want to have a preconfigured activator class.
8. (Optional) Check :code:`This plug-in will make contribution to the UI` if the plugin will contribute menus, parts, etc.
9. Select :code:`Next`
10. Uncheck :code:`Create plug-in using one of the templates`
11. Select :code:`Finish`

At this point you have a simple plugin project. But it will not be included in the
binaries of InSilico. That's because InSilico is a Eclipse RCP product which is based
on features, not on plugins. You have to add your newly created plugin to an existing
feature or create a new one (TODO add link). If you launch InSilico from Eclipse it will
detect your plugin and add it to the bundle cache. But the maven build will still
fail. To solve this problem we have to create a new :code:`pom.xml` file and fill it with the
needed informations.

1. Right click on your plugin project
2. Select :code:`File > New > File`
3. Name it :code:`pom.xml`
   - Ensure your project folder is entered in the top textfield.
4. Select :code:`Finish`
5. Open :code:`pom.xml`
6. Copy and paste the template from below and insert the symbolic name of your bundle as :code:`artefactId`.

.. code-block:: xml

  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <!-- The parent module for every plugin -->
    <parent>
      <groupId>org.draegerlab.insilico</groupId>
      <artifactId>org.draegerlab.insilico.bundles</artifactId>
      <version>1.0.0-SNAPSHOT</version>
      <relativePath>../</relativePath>
    </parent>

    <modelVersion>4.0.0</modelVersion>
    <!-- Insert the symbolic name of your plugin here -->
    <artifactId> XXX </artifactId>
    <name> InSilico - Launcher Model</name>
    <packaging>eclipse-plugin</packaging>

    <build>
      <sourceDirectory>src</sourceDirectory>

      <!-- Tells maven to add the META-INF folder into the resulting jar.
      This folder contains the required MANIFEST.MF file. -->
      <resources>
        <resource>
          <directory>.</directory>
          <includes>
            <include>META-INF/</include>
          </includes>
        </resource>
      </resources>

      <!-- Adds the maven tycho plugin to this project. -->
      <plugins>
        <plugin>
          <groupId>org.eclipse.tycho</groupId>
          <artifactId>tycho-source-plugin</artifactId>
          <version>${tycho.version}</version>
        </plugin>
      </build>
    </project>

After these steps your project contains all the information maven needs to build your plugin.
But there's still one final piece missing: Every time we build InSilico using Maven Tycho
we want the our new plugin to be included in that build. To do so we will make
our new project a submodule of InSilico.

1. Open :code:`insilico/bundles/pom.xml`
2. Find the :code:`<modules>` tag
3. Insert :code:`<module> XYZ </module>` after the opening tag
4. Replace :code:`XYZ` with the relative location of your plugin project folder
   - If you followed the recommended style you will have to insert the symbolic name of your plugin

Verify the setup by running :code:`mvn clean verify` in the root project of InSilico.
When the build succeeds you should see the name or the symbolic name of your plugin in the
final result list.


Create A Plugin From A Maven Dependency
=======================================

Declare A OSGi Service
======================

Contribute To The UI
====================
