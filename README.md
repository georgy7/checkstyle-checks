## My Checkstyle Configuration

This is a battle-tested [Checkstyle](https://checkstyle.org/) configuration
designed to help you write clean, readable, and maintainable Java code.

If you:

- want a **consistent code style** across your team,
- are tired of endless formatting debates,
- want to **catch bugs early — before code reviews**,

this config is a great starting point.

It’s based on the classic [`sun_checks`](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/sun_checks.xml),
but has been refined through real-world use and practical experience.
The config is used in real projects and is updated as new versions of Checkstyle are released.

### What's in this config:

- Prohibits magic numbers
- Checks utility classes without a constructor to avoid accidental instantiation
- Allows parameters without `final`
- Allows the ternary operator

### How to use

#### Maven

1. Copy `checkstyle.xml` and `checkstyle-suppressions.xml` to the project root.
2. Configure the Checkstyle plugin in your `pom.xml`:

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

After configuration, run:
```bash
mvn checkstyle:check
```

#### Gradle

1. Create the directory `config/checkstyle` in your project root (if it doesn't exist).
2. Place `checkstyle.xml` and `checkstyle-suppressions.xml` into `config/checkstyle/`.
3. Apply the Checkstyle plugin in `build.gradle`:

    ```gradle
    plugins {
        // other plugins...
        id 'checkstyle'
    }

    checkstyle {
        toolVersion = '10.20.0'
    }
    ```

Then run:
```bash
./gradlew checkstyleMain
./gradlew checkstyleTest
```

> [!TIP]
> You can also run `./gradlew check` to execute all verification tasks, including Checkstyle.

### Links

- [Sun Java Style](https://checkstyle.sourceforge.io/sun_style.html)
- [Sun checks](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/sun_checks.xml)
- [Google Java Style](https://checkstyle.sourceforge.io/google_style.html)
- [Google checks](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml)
- [Maven Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)
- [Gradle Checkstyle Plugin](https://docs.gradle.org/current/userguide/checkstyle_plugin.html)
