# Generate GraalVM native image with Maven

## Getting Started

```
$ sdk install java 19.2.0-grl
$ sdk install maven 3.6.1
```

## Java Code

```java
package com.buralo.demo.graalvm.hello;

public class Main {

    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

## POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.buralo.demo.graalvm</groupId>
    <artifactId>demo-graalvm-hello</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
            <plugin>
                <groupId>com.oracle.substratevm</groupId>
                <artifactId>native-image-maven-plugin</artifactId>
                <version>19.2.0</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>native-image</goal>
                        </goals>
                        <phase>package</phase>
                        <configuration>
                            <mainClass>com.buralo.demo.graalvm.hello.Main</mainClass>
                            <imageName>demo-graalvm-hello</imageName>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

## Build

```
$ sdk use java 19.2.0-grl
$ sdk use maven 3.6.1
$ mvn clean package
$ ./target/demo-graalvm-hello
```