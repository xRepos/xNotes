---
title: SonarQube
---

SonarQube
=========

[SonarQube](http://www.sonarqube.org/)

Add JaCoCo to pom
-----------------

    #!xml
    <plugin>
        <groupId>org.jacoco</groupId>
        <artifactId>jacoco-maven-plugin</artifactId>
        <version>0.7.1.201405082137</version>
        <executions>
            <execution>
                <id>jacoco-prepare-agent</id>
                <goals>
                    <goal>prepare-agent</goal>
                </goals>
            </execution>
            <execution>
                <id>jacoco-report</id>
                <goals>
                    <goal>report</goal>
                </goals>
            </execution>
        </executions>
    </plugin>

Build

    $ mvn clean package

* ``prepare-agent``: generate result in ``target/jacoco.exec``
* ``report``: create report based on ``jacoco.exec``, into ``target/site/jacoco``

Run Sonar
---------

    $ mvn sonar:sonar

Add params:

    
    $ mvn sonar:sonar -Dsonar.host.url=http://x.x.x.x:8080/ -Dsonar.jdbc.url=jdbc:mysql://x.x.x.x:3306/<db_name> -Dsonar.jdbc.username=<user_name> -Dsonar.jdbc.password=<password>

