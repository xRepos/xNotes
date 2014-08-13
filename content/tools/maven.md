---
title: Apache Maven
description: 
---

Apache Maven
============

Release
-------

### Prepare

It will update version to release version, tag code, commit and push. Meanwhile generate pom.xml.backup and release.proprerties files in the current dir.

    $ mvn release:prepare

### Perform

It will deploy package to nexus, checkout the tag code to local and update version to [new version]-SNAPSHOT, and cleanup the backup&properties files.

    $ mvn release:perform

Update Version
--------------

    $ mvn versions:set -DnewVersion=``release version``

Install Package
---------------

    $ mvn install:install-file -Dfile=<path-to-file> -DgroupId=<group-id> \
        -DartifactId=<artifact-id> -Dversion=<version> -Dpackaging=<packaging>


Set Main-Class
--------------

    #!xml
    <build>
        <defaultGoal>compile</defaultGoal>

        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>your.main.class</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>

Copy Dependencies
-----------------

    #!xml
    <build>        
        <plugins>          
            <plugin>            
                <artifactId>maven-dependency-plugin</artifactId>            
                <executions>              
                    <execution>                
                        <phase>install</phase>                
                        <goals>                     
                            <goal>copy-dependencies</goal>                
                        </goals>                
                        <configuration>                  
                            <outputDirectory>${project.build.directory}/lib</outputDirectory>                
                        </configuration]]>              
                    </execution>            
                </executions>          
            </plugin>        
        </plugins>      
    </build>

maven-assembly-plugin
---------------------

If the following descriptor is set, the final jar will be ProjectName-Version-jar-with-dependencies.jar

    #!xml
    <descriptorRefs>
        <descriptorRef>jar-with-dependencies</descriptorRef>
    </descriptorRefs>

Full example:

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>2.4.1</version>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

To set the final name: 

    #!xml
    <configuration>
        <finalName>FinalName</finalName>
        ...
    </configuration>

To remove the suffix:

    #!xml
    <configuration>
        <appendAssemblyId>false</appendAssemblyId>
        ...
    </configuration>

Recursively add files
---------------------

    #!xml
    <fileSet>
        <directory>${project.basedir}/src/test/resources/examples</directory>
        <outputDirectory>/examples</outputDirectory>
        <includes>
            <include>**/*</include>
        </includes>
    </fileSet>

Multiple Excution
-----------------

    #!xml
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>2.3</version>
                
                <executions>
                    <execution>
                        <id>make-jar</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <archive>
                                <manifest>
                                    <mainClass>your.main.class</mainClass>
                                </manifest>
                            </archive>
                            <descriptorRefs>
                                <descriptorRef>jar-with-dependencies</descriptorRef>
                            </descriptorRefs>
                            <finalName>FinalName</finalName>
                            <appendAssemblyId>false</appendAssemblyId>
                        </configuration>
                    </execution>
                    
                    <execution>
                        <id>make-assembly</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <descriptors>
                                <descriptor>assembly.xml</descriptor>
                            </descriptors>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

Set Dependency As Optional
--------------------------

Assume Project-A depends on ``slf4j``, ``Project-B`` depends on ``Project-A``, then ``slf4j`` will not be treated as dependency in ``Project-B``; ``slf4j`` must be added to ``Project-B``'s pom in order to be used 

    #!xml
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.7.7</version>
        <optional>true</optional>
    </dependency>
