---
layout: post
title:  "Create an executable jar with dependencies using maven"
date:   2016-03-28 16:50:03 +0800
categories: maven
---

<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-dependency-plugin</artifactId>
    <executions>
        <execution>
            <id>copy-dependencies</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>copy-dependencies</goal>
            </goals>
            <configuration>
                <outputDirectory>${project.build.directory}/lib</outputDirectory>
                <overWriteReleases>false</overWriteReleases>
                <overWriteSnapshots>false</overWriteSnapshots>
                <overWriteIfNewer>true</overWriteIfNewer>
            </configuration>
        </execution>
    </executions>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-jar-plugin</artifactId>
    <configuration>
        <archive>
            <manifest>
                <addClasspath>true</addClasspath>
                <classpathPrefix>lib/</classpathPrefix>
                <mainClass>theMainClass</mainClass>
            </manifest>
        </archive>
    </configuration>
</plugin>

参考：<a href="http://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven" target="_blank">http://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven</a>
