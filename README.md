asynchbase-shaded
=================

This project creates a shadow jar of [asynchbase](https://github.com/OpenTSDB/asynchbase) where the following transitive dependencies are relocated to avoid classpath collisions that can happen easily in Apache Hadoop and Spark environments.

* `com.google` → `org.apache.s2graph.google` : Google Guava and Protocol Buffers
* `org.jboss` → `org.apache.s2graph.jboss` : Contains Netty 3.9.4.Final

The jar also packages [async](https://github.com/OpenTSDB/async), and ignores `org.jboss.netty:netty:3.2.2.Final` that is pulled by zookeeper in favor of the newer version; Netty has a backward compatibility in its 3.x versions. The resulting POM will have zookeeper and slf4j-api as its transitive dependencies, which are excluded from the shadow jar.

## Building

This project uses [Gradle Shadow plugin](https://github.com/johnrengelman/shadow) that can be built using

    $ ./gradlew shadow
    
The resulting jar will be located at `./build/libs/asynchbase-shaded.jar`, and can be installed in `~/.m2` with

    $ ./gradlew publishToMavenLocal
    
