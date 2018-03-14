=======
Plugins
=======

A Plugin is a OSGi Bundle with a additional `plugin.xml` file.

Create A New Plugin
===================

1. Select :code:`File > New > Project..`
2. Select :code:`Plug-in Development > Plug-in Project`
3. Enter the name of the Plugin
   a. The name should match the symbolic name of the plugin
4. Uncheck :code:`Use default location`
5. Enter the location for the plugin
   a. The plugin project should be located in :code:`insilico/bundles`
   b. The name of the folder should match the symbolic name of the plugin
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
fail. To solve this problem we have to create a new `pom.xml` file and fill it with the
needed informations.

1. Right click on your plugin project
2. Select :code:`File > New > File`
3. Name it :code:`pom.xml`
  a. Ensure your project folder is entered in the top textfield.
4. Select :code:`Finish`
5. Open :code:`pom.xml`
6. Copy and Paste the template from below

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

After these steps you will have created a minimalistic plugin project. You may want to add some
dependencies to your plugin or declare some extensions / extension points.

Dependencies
============

Declare your dependencies in the :code:`MANIFEST.MF` file. You should use the
Eclipse Editor for this.

Extensions
==========

You can declare extensions to an existing extension point via the :code:`plugin.xml` file.
That's also where you expose your own extension points.
It's recommended to use the Eclipse Editor for this task.
