# Maven Support

[← Back to API Index](../reference.md)

---

## KB Topic: Maven Support

### Description
SmartClient artifacts are not published to any public repository, but a POM for each is included in the SDK, and can be used to install them to your own private Maven repository. The official [Isomorphic plugin for Maven](http://github.smartclient.com/isc-maven-plugin/) contains a handful of targets intended to simplify that process through automation. Please refer to the plugin's documentation for usage and examples.

For a complete listing of artifacts installed in your environment, consult your repository manager. Where no repository manager is in use, a directory listing of your local repository can often provide all the detail you need. Once you've made an artifact available to your build, you can use it just like you'd use any other dependency.

That said, typical installations of the current build will include the artifacts documented [here](./mavendoc/maven-usage.html), where coordinates in most cases will vary slightly by date and license. A sample configuration using a few artifacts from an eval build released on November 14, 2016 follows:

```
 <?xml version="1.0" encoding="UTF-8"?>
 <project  xmlns="http://maven.apache.org/POM/4.0.0" 
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 
      <modelVersion>4.0.0</modelVersion>
 
      <groupId>com.isomorphic.smartclient.samples</groupId>
      <artifactId>component-databinding</artifactId>
      <version>1.0.0</version>
      <packaging>war</packaging>
 
      <dependencies>
 
          <!-- The SmartClient Evaluation edition -->
          <dependency>
              <groupId>com.isomorphic.smartclient.eval</groupId>
              <artifactId>smartclient-eval</artifactId>
              <version>11.0-p20161114</version>
              <type>pom</type>
          </dependency>
 
          <!-- Use SQLDataSources -->
          <dependency>
              <groupId>com.isomorphic.smartclient.eval</groupId>
              <artifactId>isomorphic-sql</artifactId>
              <version>11.0-p20161114</version>
          </dependency>

      </dependencies>
 </project>
 
```

Following execution of the plugin's install or deploy goal, its [working directory](http://github.smartclient.com/isc-maven-plugin/install-mojo.html#workdir) will contain a copy of the SDK that you can use to view doc and samples locally. Your Maven repository will also include a handful of archetypes meant to jump start development with the SmartClient framework. Most users will want to start new projects with either the **archetype-smartclient-quickstart** or **archetype-smartclient-quickstart-relogin** archetypes. To generate a new project based on the former:

1.  [Install Maven](https://maven.apache.org/install.html), if necessary.
2.  Install SmartClient, if necessary. _Note that when copy/pasting commands, you may need to substitute the backslash with the appropriate character to escape new lines in your command-line interface (eg: `^` for Windows command-line, `` ` `` for PowerShell, etc)._
    ```
     mvn com.isomorphic:isc-maven-plugin:1.4.5:install \
        -Dproduct=SMARTCLIENT -Dlicense=EVAL -DbuildNumber=${ENV:SC_VERSION}
     
    ```
    
3.  Generate a project (using LATEST as below, or the version installed for you in step 2)
    ```
      mvn archetype:generate \
        -DartifactId=my-application \
        -Dmodule=MyApplication -Dmodule-short-name=myapp \
        -DgroupId=com.example -Dpackage=com.example.myapplication \
        -DarchetypeGroupId=com.isomorphic.archetype \
        -DarchetypeArtifactId=archetype-smartclient-quickstart \
        -DarchetypeVersion=LATEST -DinteractiveMode=false
     
    ```
    

and refer to the README in the new 'my-application' directory for further instructions around usage in Maven, Ant, and Eclipse environments.

To generate a project from any of the following archetypes, provide its artifactId to the above command's archetypeArtifactId parameter:

*   **archetype-smartclient-quickstart**: The recommended approach for most applications, using data access / databinding with "sql" datasources
*   **archetype-smartclient-quickstart-relogin**: Like archetype-smartclient-quickstart, but includes integration with Spring Security to illustrate the [relogin](relogin.md#kb-topic-relogin) pattern.

---
