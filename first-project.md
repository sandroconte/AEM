# Creating an Adobe Experience Manager 6.3 Project using Adobe Maven Archetype 11
## Introduction
This development article walks you through creating an AEM 6.3 project by using Archetype 11 and explains the default AEM files and services. Using an Archetype 11 project, you are given a set of files to start with:

* 2 Pages: English and French pages with filler text

* 2 Templates: 
  * For homepage and content pages
  * Homepages are only allowed on top level, and content pages below

* Page component
  * Built with HTL templates and simple server-side JavaScript logic
  * The CSS class on the body element changes based on page template
  * Internationalized footer text as example

* Structure Components
  * Topnav: simple custom HTL component
  * Logo: based on foundation

* Content Components
  * helloworld: example of custom HTL component with SlingModels for the logic 
  * colctrl, textimage, text, image,
  * title: use the HTL foundation components

* Configurations
  * Device emulators displayed in the authoring interface
  * Allow direct drag & drop of assets from the content finder into parsys (6.1 TouchUI)
  * Dictionnary structure for internationalizing hardcoded strings

* Client libraries
  * Responsive layout with colctr that break for narrow pages
  * CSS class names follow AEM naming conventions
  * Component-specific styles stored within each component
  * Master ClientLib under /etc/designs merges all client libraries into one file

* Bundle with some examples
  * Models: Models for more complex business logic of components
  * Servlets: Rendering the output of specific requests
  * Filters: Applied to the requests before dispatching to the servlet or script
  * Schedulers: Cron-job like tasks

* Tests
  * Unit tests
  * Integration tests
  * Client-side Hobbes tests within developer mode

# Create an AEM Maven 11 archetype project
To create an Experience Manager archetype project, perform these steps:

1. Open the command prompt and go to your working directory (for example, C:\AdobeCQ).

2. Run the following Maven command:
```
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeGroupId=com.adobe.granite.archetypes -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=11 -DarchetypeCatalog=https://repo.adobe.com/nexus/content/groups/public/
```
3. When prompted, specify the following information:
* groupId - AEM63App
* artifactId - AEM63App
* version - 1.0-SNAPSHOT
* package - com.aem.community
* appsFolderName - AEM63App
* artifactName - AEM63App
* componentGroupName - AEM63App
* contentFolderName - AEM63App
* cssId - AEM63App
* packageGroup - AEM63App
* siteName - AEM63App

4. WHen prompted, specify Y.
5. Once done, you will see a message like:
```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 01:42 min
[INFO] Finished at: 2016-04-25T14:34:19-04:00
[INFO] Final Memory: 16M/463M
[INFO] ------------------------------------------------------------------------
```
6. Change the working directory to AEM63App and then enter the following command.
```
mvn eclipse:eclipse
```
After you run this command, you can import the project into Eclipse as discussed in the next section.

## Add Java files to the Maven project using Eclipse
To make it easier to work with the Maven generated project, import it into the Eclipse development environment, as shown in the following illustration.

![eclipse-import-project](https://helpx.adobe.com/content/dam/help/en/experience-manager/using/maven_arch11/_jcr_content/main-pars/image_915987931/project.png)

** Note: ** Do not worry about the errors reported in Eclipse. It does not read the POM file where the APIs are resolved. You build the bundle with Maven. Eclipse is used to edit the Java files and the POM file.

### After you import the project into Eclipse, notice each module is a separate Eclipse project:

* **core** - where Java files that are used in OSGi services and sling servlets are located
* **launcher** - where additional Java files are located
* **tests** - Java files for tests like JUNIT tests
* **apps** - content under /apps
* **content** - content under /content

When you want to create an OSGi service, you work under core. Likewise, if you want to create a HTL component, you can work under apps.
By default, the Archetype 11 project creates a number of Java files that you can use as a starting point in your project (these Java files are located under core).
The following illustration shows the packages.

![eclipse-scaffolding-project](https://helpx.adobe.com/content/dam/help/en/experience-manager/using/maven_arch11/_jcr_content/main-pars/image_215937034/java.png)

**Rif.** [Creating an Adobe Experience Manager 6.3 Project using Adobe Maven Archetype 11](https://helpx.adobe.com/experience-manager/using/maven_arch11.html)
