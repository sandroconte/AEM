# Set up a Local AEM Development Environment
## Overview
Setting up a local development environment is the first step when developing for Adobe Experience Manager or AEM. Take the time to set up a quality development environment to increase your productivity and write better code, faster. We can break an AEM local development environment into 4 areas:
* Local AEM instances
* Apache Maven project
* Integrated Development Environments (IDE)
* Troubleshooting

## Install Apache Maven
Apache Maven is a tool to manage the build and deploy procedure for Java-based projects. AEM is a Java-based platform and Maven is the standard way to manage code for an AEM project. When we say AEM Maven Project or just your AEM Project , we are referring to a Maven project that includes all of the custom code for your site.
All AEM projects should be built off the latest version of the AEM Project Archetype : https://github.com/Adobe-Marketing-Cloud/aem-project-archetype . The AEM Project Archetype will create a bootstrap of an AEM project with some sample code and content. The AEM Project Archetype also includes AEM WCM Core Components configured to be used on your project.
1. Download [Apache Maven] (https://maven.apache.org/download.cgi)
2. Install !DNL[Apache Maven] (https://maven.apache.org/install.html) and ensure that the installation has been added to your command-line PATH .
3. Verify that Maven is installed by opening a new command line terminal and executing the following:
```
$ mvn --version
Apache Maven 3.3.9
Maven home: /Library/apache-maven-3.3.9
Java version: 1.8.0_111, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
```
4. Add the adobe-public profile to your Maven [settings.xml](https://maven.apache.org/settings.html) file in order to automatically add repo.adobe.com to the maven build process.
5. Create a file named settings.xml at ~/.m2/settings.xml if it doesn't exist already.
6. Add the adobe-public profile to the settings.xml file based on the [instructions here](https://repo.adobe.com/) .
A sample settings.xml is listed below. Note, the naming convention of settings.xml and the placement beneath the user's .m2 directory is important.
```
<settings xmlns="https://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0
                      https://maven.apache.org/xsd/settings-1.0.0.xsd">
<profiles>
 <!-- ====================================================== -->
 <!-- A D O B E   P U B L I C   P R O F I L E                -->
 <!-- ====================================================== -->
     <profile>
         <id>adobe-public</id>
         <activation>
             <activeByDefault>true</activeByDefault>
         </activation>
         <properties>
             <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
             <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
             <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
         </properties>
         <repositories>
             <repository>
                 <id>adobe-public-releases</id>
                 <name>Adobe Public Repository</name>
                 <url>https://repo.adobe.com/nexus/content/groups/public</url>
                 <releases>
                     <enabled>true</enabled>
                     <updatePolicy>never</updatePolicy>
                 </releases>
                 <snapshots>
                     <enabled>false</enabled>
                 </snapshots>
             </repository>
         </repositories>
         <pluginRepositories>
             <pluginRepository>
                 <id>adobe-public-releases</id>
                 <name>Adobe Public Repository</name>
                 <url>https://repo.adobe.com/nexus/content/groups/public</url>
                 <releases>
                     <enabled>true</enabled>
                     <updatePolicy>never</updatePolicy>
                 </releases>
                 <snapshots>
                     <enabled>false</enabled>
                 </snapshots>
             </pluginRepository>
         </pluginRepositories>
     </profile>
</profiles>
 <activeProfiles>
     <activeProfile>adobe-public</activeProfile>
 </activeProfiles>
</settings>
```
7. Verify that the adobe-public profile is active by running the following command:
```
$ mvn help:effective-settings
...
<activeProfiles>
    <activeProfile>adobe-public</activeProfile>
</activeProfiles>
<pluginGroups>
    <pluginGroup>org.apache.maven.plugins</pluginGroup>
    <pluginGroup>org.codehaus.mojo</pluginGroup>
</pluginGroups>
</settings>
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.856 s
```
## [Set Up an Integrated Development Environment](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)

Follow the instructions on [eclipse adobe plugin](https://eclipse.adobe.com/aem/dev-tools/) for installing the Adobe plugin for Eclipse

### Next step: [Adobe plugin installation setup on Eclipse](https://video.tv.adobe.com/v/25906?quality=12)
