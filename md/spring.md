# Learning to use Spring

## Steps
* Start with maven
  * ```mvn archetype:generate -DgroupId=za.co.catenare.tutorial -DartifactId=tutorial -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false```
  * cd tutorial
  * mvn package
  * java -cp target/tutorial-1.0-SNAPSHOT.jar za.co.catenare.tutorial.App
    * Runs the App
