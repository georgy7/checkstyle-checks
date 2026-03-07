## My checkstyle configuration

These are [checkstyle](https://checkstyle.org/) configuration files I use in my Java projects. 

They are based on the original [sun checks](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/sun_checks.xml) 
and have been changed to match my practical experience. The rule set has been updated by removing certain checks
(e.g., _FinalParameters_ or _AvoidInlineConditionals_) and adding others (e.g., _MagicNumber_ or _HideUtilityClassConstructor_).
They also contain some comments that explain the purpose of particular rules and why certain parameters were chosen.

The files are continuously updated as new checkstyle versions release and my experience evolves.

### Usage

Here are examples of using these configuration files in Maven and Gradle:

#### Maven

1) Copy `checkstyle.xml` and `checkstyle-suppressions.xml` to the project root
2) Configure checkstyle plugin as following:
    ```xml
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-checkstyle-plugin</artifactId>
        <version>3.6.0</version>
        <dependencies>
            <dependency>
                <groupId>com.puppycrawl.tools</groupId>
                <artifactId>checkstyle</artifactId>
                <version>12.0.1</version>
            </dependency>
        </dependencies>
        <configuration>
            <configLocation>checkstyle.xml</configLocation>
            <includeTestSourceDirectory>true</includeTestSourceDirectory>
            <consoleOutput>true</consoleOutput>
            <failsOnError>true</failsOnError>
        </configuration>
        <executions>
            <execution>
                <id>validate</id>
                <phase>validate</phase>
                <goals>
                    <goal>check</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
    ```
then use
```bash
mvn checkstyle:check
```

#### Gradle

1) Put `checkstyle.xml` and `checkstyle-suppressions.xml` into `/config/checkstyle` directory of your project
2) Configure `build.gradle`:
    ```gradle
    plugins {
        ...
        id 'checkstyle'
    }
    
    checkstyle {
        toolVersion = '10.20.0'
    }
    ```
then use
```bash
gradle checkstyleMain
gradle checkstyleTest
```

### Links

- [Sun Java Style](https://checkstyle.sourceforge.io/sun_style.html)
- [Sun checks](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/sun_checks.xml)
- [Google Java Style](https://checkstyle.sourceforge.io/google_style.html)
- [Google checks](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml)
- [Maven Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)
- [Gradle Checkstyle Plugin](https://docs.gradle.org/current/userguide/checkstyle_plugin.html)