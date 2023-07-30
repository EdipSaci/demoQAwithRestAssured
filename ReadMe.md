# CitizenM task

This project is a QA automation framework built using Cucumber BDD (Behavior-Driven Development) framework with Selenium. It provides a structured approach for automating browser tests, ensuring efficient test case management and easier collaboration between QA engineers and stakeholders. Maven as the build automation tool for managing dependencies and executing tests. JUnit for assertion and validation of test results. There is two main step for this framework


### Steps to Create Project
#### 1.Create a maven project called `demoQAWtihRestAssured`

#### 2.Under `pom.xml`

>> 1.add below property section

```xml

<properties>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

>> 2.Add dependencies

```xml
<dependencies>

     <dependency>
          <groupId>org.seleniumhq.selenium</groupId>
          <artifactId>selenium-java</artifactId>
          <version>3.141.59</version>
     </dependency>

     <!-- https://mvnrepository.com/artifact/io.github.bonigarcia/webdrivermanager -->
     <dependency>
          <groupId>io.github.bonigarcia</groupId>
          <artifactId>webdrivermanager</artifactId>
          <version>5.3.1</version>
     </dependency>
     
     <!-- https://mvnrepository.com/artifact/io.cucumber/cucumber-java -->
     <dependency>
          <groupId>io.cucumber</groupId>
          <artifactId>cucumber-java</artifactId>
          <version>7.2.3</version>
     </dependency>

     <!-- https://mvnrepository.com/artifact/io.cucumber/cucumber-junit -->
     <dependency>
          <groupId>io.cucumber</groupId>
          <artifactId>cucumber-junit</artifactId>
          <version>7.2.3</version>
          <scope>test</scope>
     </dependency>

     <dependency>
          <groupId>me.jvt.cucumber</groupId>
          <artifactId>reporting-plugin</artifactId>
          <version>7.2.0</version>
     </dependency>

     <!-- https://mvnrepository.com/artifact/com.github.javafaker/javafaker -->
     <dependency>
          <groupId>com.github.javafaker</groupId>
          <artifactId>javafaker</artifactId>
          <version>1.0.2</version>
     </dependency>

     <!--If you want to get rid of SLF4J Failed to load message from the console -->
     <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-simple</artifactId>
          <version>1.7.32</version>
     </dependency>

     <dependency>
          <groupId>org.junit.jupiter</groupId>
          <artifactId>junit-jupiter</artifactId>
          <version>5.7.2</version>
     </dependency>

     <dependency>
          <groupId>io.rest-assured</groupId>
          <artifactId>rest-assured</artifactId>
          <version>4.4.0</version>
     </dependency>

     <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
     <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.14.2</version>
     </dependency>


     <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.18.26</version>
     </dependency>
     
</dependencies>
 ```

>> 3.Add Build Plugins

```xml
<build>

     <plugins>
          <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-surefire-plugin</artifactId>
               <version>3.0.0-M5</version>
               <configuration>
                    <parallel>methods</parallel>
                    <!--<useUnlimitedThreads>true</useUnlimitedThreads>-->
                    <threadCount>4</threadCount>
                    <testFailureIgnore>true</testFailureIgnore>
                    <includes>
                         <include>**/CukesRunner*.java</include>
                    </includes>
               </configuration>
          </plugin>
     </plugins>
</build>

```
>

#### 4.Create a package called `com.demoQAUI` under `src/test/java`

> 1. under `com.demoQAUI`, create `pages`, `runners`, `srep_definitions` and `utilities `packages 

> 2. Add a `configuration.properties` file to store project information in order to avoid hard coding.
     add following information:
```
browser=chrome
username=johnWick
password=Pass471!
url=https://demoqa.com/
```


#### 5.Create `resources directory` under project level 
> 1. Create a file with `.feature` extension to define scenarios and steps. This just a regular file.

> 2. In feature file follow cucumber BDD (Gherkin) approach



#### 6.In order to generate test report, we need to use maven goal

if you are using command line: mvn clean verify cmd+enter or ctrl+enter. if you dont have maven installed locally and
if you are using IntelliJ buttons;
first click on clean then click on verify.
Your report will be generated under target as HTML Report

#### 7.Under `step_definitions` package, create feature file corresponding `java classes` to write test source code

> 1. Create `Hooks` java class to use cucumber `@Before` and `@After` annotations


#### 8.Under `runners` package, create `CukesRunner` and `FailedTestRunner` java classes to run `step_definitions` java classes test source code
> 1. Add below information above CukesRunner class name
```
@RunWith(Cucumber.class)
@CucumberOptions(
        plugin = {
                //"pretty",
                "html:target/cucumber-report.html",
                "rerun:target/rerun.txt",
                "me.jvt.cucumber.report.PrettyReports:target/cucumber",
                "json:target/cucumber.json"
        },

        features = "src/test/resources/features",
        glue = "com/demoQAUI/step_definitions",
        dryRun =,
        tags = ""
)
```
> 2. Add below information above FailedTestRunner class name
```
@RunWith(Cucumber.class)
@CucumberOptions(
        glue = "com/demoQAUI/step_definitions",
        features = "@target/rerun.txt"
)
```

#### 10.Under `pages` package, create each page of application corresponding `Java Classes` to store each page related web elements to achieve Page Object Model
> 1. Create BasePage java class and add base page class constructor with following 
```
 public BasePage() {
        PageFactory.initElements(Driver.getDriver(),this);
    }
```


#### 11.For API Testing create a package called `com.demoQAAPI` under `src/test/java`
> 1. Create pojo package to store POJO classes which is implementing deserialization for each JSON file 
> 2. Improving code quality and productivity in testing by reducing repetitive tasks and enhancing the readability of test cases and test data by using Lombok library
```
@Getter
@Setter
@ToString
```

> 3. Create a test package in order to write actual code fragments



