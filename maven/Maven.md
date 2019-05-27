# Maven

<https://www.youtube.com/watch?v=t5hoD4D0Jo0>



`mvn -version`

## Maven LifeCycle

1. Maven complile
2. Maven test
3. Maven resource - jar

## Maven project 

1. create maven project

2. add dependencies

   1. testng

      ```xml
      <dependency>
          <groupId>org.testng</groupId>
          <artifactId>testng</artifactId>
          <version>6.14.3</version>
          <scope>compile</scope>
      </dependency>
      ```

   2. selenium

      ```xml
      <dependency>
          <groupId>org.seleniumhq.selenium</groupId>
          <artifactId>selenium-java</artifactId>
          <version>3.141.59</version>
      </dependency>
      ```

3. Maven clean build

   [[How to clean or clean build my Maven project in IntelliJ IDEA?](https://stackoverflow.com/questions/35409788/how-to-clean-or-clean-build-my-maven-project-in-intellij-idea)](https://stackoverflow.com/questions/35409788/how-to-clean-or-clean-build-my-maven-project-in-intellij-idea/35442639)

4. code 

   `src/test/java`

5. run test

   ```shell
   mvn clean install //build and create jar file
   
   mvn test //run test without downloading
   
   mvn package -DskipTests //only create build without running the test
   
   <properties>
   	<maven.test.skip>true</maven.test.skip>
   </properties>
   mvn package -Dmaven.test.skip=true //same as above.
   ```

6. maven update in Intellij

   `maven -> Reimport`

7. maven build plugs

   ```xml
       <build>
           <plugins>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-compiler-plugin</artifactId>
                   <version>3.8.1</version>
                   <configuration>
                       <source>1.8</source>
                       <target>1.8</target>
                   </configuration>
               </plugin>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-surefire-plugin</artifactId>
                   <version>3.0.0-M3</version>
                   <configuration>
                       <suiteXmlFiles>
                           <suiteXmlFile>src/main/resources/testng.xml</suiteXmlFile>
                       </suiteXmlFiles>
                   </configuration>
               </plugin>
               <plugin>
               <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-source-plugin</artifactId>
                   <version>2.1.1</version>
                   <executions>
                       <execution>
                           <id>attach-sources</id>
                           <phase>package</phase>
                           <goals>
                               <goal>jar-no-fork</goal>
                           </goals>
                       </execution>
                   </executions>
   
               </plugin>
           </plugins>
       </build>
   ```

8. testng.xml

   ```xml
   <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
   <suite name="Test Maven Suite">
       <test name="Test Maven Testing">
           <packages>
               <package name="com.qa.tests.*"></package>
           </packages>
       </test>
   </suite>
   ```

   