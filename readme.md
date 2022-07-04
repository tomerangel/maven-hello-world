DevOps Exercise -- tomerangel

a.	Which programming language is this?  - java

b.	What is maven?  - Maven is a powerful build automation tool that is primarily used for java based projects maven address two critical aspects of building software first it describes how software is built and second it describes dependencies it uses conventions for build procedure and only exception need to be written down an XML file (POM file)

c.	How does maven work? -- Main Goals of Maven

Making the build process unified
Providing project information
Based on your pom configuration Maven knows how to build your project. With the project information it is capable of downloading the defined dependencies from the maven repository and bundling them with your application.

How does a Maven Build work?
Maven has three build lifecycles:

default (project deployment)
clean (project cleaning)
site (creates project’s site documentation)
All lifecycles consist of different build phases. The default lifecycle for example consist of these build phases:

validate
compile
test
package
verify
install
deploy
You can define different goals for each build phase in your pom.xml file. Goals perform the action required to make the build. The Java class files which define a goal are called Mojo (Maven plain Old Java Object). Each Mojo is an executable goal which can be configured within the pom.xml file. A Maven Plugin on the other contains one or more Mojos.

On the command line you can say which of these lifecycles you want to execute. You can even specify which build phase or which goal you want to start. Based on your configuration Maven the figures out what actions need to be performed.

d.	What is this pom.xml everyone keeps mentioning?  -- A Project Object Model or POM is the fundamental unit of work in Maven. It is an XML file that contains information about the project and configuration details used by Maven to build the project. It contains default values for most projects.


_____________________________________________________________________________________________________________________________________________________________________
ALL FROM FORK
# A simple, minimal Maven example: hello world

To create the files in this git repo we've already run `mvn archetype:generate` from http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

Now, to print "Hello World!", type either...

    cd my-app
    mvn compile
    java -cp target/classes com.mycompany.app.App

or...

    cd my-app
    mvn package
    java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App

Running `mvn clean` will get us back to only the source Java and the `pom.xml`:

    murphy:my-app pdurbin$ mvn clean --quiet
    murphy:my-app pdurbin$ ack -a -f
    pom.xml
    src/main/java/com/mycompany/app/App.java
    src/test/java/com/mycompany/app/AppTest.java

Running `mvn compile` produces a class file:

    murphy:my-app pdurbin$ mvn compile --quiet
    murphy:my-app pdurbin$ ack -a -f
    pom.xml
    src/main/java/com/mycompany/app/App.java
    src/test/java/com/mycompany/app/AppTest.java
    target/classes/com/mycompany/app/App.class
    murphy:my-app pdurbin$ 
    murphy:my-app pdurbin$ java -cp target/classes com.mycompany.app.App
    Hello World! tomer angel

Running `mvn package` does a compile and creates the target directory, including a jar:

    murphy:my-app pdurbin$ mvn clean --quiet
    murphy:my-app pdurbin$ mvn package > /dev/null
    murphy:my-app pdurbin$ ack -a -f
    pom.xml
    src/main/java/com/mycompany/app/App.java
    src/test/java/com/mycompany/app/AppTest.java
    target/classes/com/mycompany/app/App.class
    target/maven-archiver/pom.properties
    target/my-app-1.0-SNAPSHOT.jar
    target/surefire-reports/com.mycompany.app.AppTest.txt
    target/surefire-reports/TEST-com.mycompany.app.AppTest.xml
    target/test-classes/com/mycompany/app/AppTest.class
    murphy:my-app pdurbin$ 
    murphy:my-app pdurbin$ java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
    Hello World! tomer angel

Running `mvn clean compile exec:java` requires http://mojo.codehaus.org/exec-maven-plugin/

Running `java -jar target/my-app-1.0-SNAPSHOT.jar` requires http://maven.apache.org/plugins/maven-shade-plugin/
