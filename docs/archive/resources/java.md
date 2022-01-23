# Java Notes
1. Determine location of Java on Mac OS X
    1. ```echo $(/usr/libexec/java_home)```
1. Using Ivy with Ant
    * Download [Apache Ivy](http://ant.apache.org/ivy/)
        1. Put files into ant/lib directory.
        1. Lib directory at `~/.ant/lib` - Using sdkman to manage Ant.

## Resources
* [Awesome Java](https://github.com/akullpp/awesome-java)
* [JHipster](jhipster) - Spring Boot + Angular
* [Lombok](https://projectlombok.org/) - decorators for Java.
* [Apache POI](https://poi.apache.org/) - API for Microsoft Documents
* [Java Design Patterns](https://github.com/iluwatar/java-design-patterns)
* [Jbake](http://jbake.org/) - Static site generator in Java
* [Apache FOP](https://xmlgraphics.apache.org/fop/) - PDF generator
* [DropWizard](http://www.dropwizard.io/1.2.0/docs/) - Generate REST Apps.
* [Handlebars Java](https://jknack.github.io/handlebars.java/) - Mustache/Handlebars template engine in Java.
* [Apache PDFBox](https://pdfbox.apache.org/) - java library for PDF
* [Java Sample Approach](http://javasampleapproach.com/)

# JHipster
## Resources
* [JHipster](http://www.jhipster.tech/) - Spring Boot + Angular
* [JHipster Book](http://www.jhipster-book.com/#!/)
* Articles and Tutorials
	* [Top 10 JavaOne 2017 Sessions for Java Hipsters](https://developer.okta.com/blog/2017/09/28/top-10-javaone-2017-sessions-for-java-hipsters)
	* [Microservices with JHipster](https://developer.okta.com/blog/2017/06/20/develop-microservices-with-jhipster)
* People
	* [Matt Raible](https://github.com/mraible)
## Dev Notes
* [Tell Gradle to use a specific jdk version](https://stackoverflow.com/questions/18487406/how-do-i-tell-gradle-to-use-specific-jdk-version) = Point to Java8 -
    * In *gradle.properties* - on Mac OS X with SDKMAN installed
    `org.gradle.java.home=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home`

# Learning to use Spring
## Steps
* Start with maven
  * ```mvn archetype:generate -DgroupId=za.co.catenare.tutorial -DartifactId=tutorial -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false```
  * cd tutorial
  * mvn package
  * java -cp target/tutorial-1.0-SNAPSHOT.jar za.co.catenare.tutorial.App
    * Runs the App
