## Basic Maven Questions

1. **What is Maven?**
   - Maven is a build automation tool primarily used for Java projects. It simplifies the build process by managing dependencies, building and packaging the application, and running tests. It uses an XML file (`pom.xml`) to define project configurations, dependencies, and goals.

2. **What is a POM (Project Object Model) in Maven?**
   - POM is an XML file (`pom.xml`) that contains configuration details for your Maven project. It defines the project's structure, dependencies, plugins, and other settings that Maven uses to build the project.

3. **What is the role of `pom.xml`?**
   - `pom.xml` is the heart of a Maven project. It defines the project's dependencies, plugins, build settings, goals, and other configurations. It is used by Maven to manage the build lifecycle, fetch dependencies, and configure the build process.

4. **What are the different phases in the Maven build lifecycle?**
   - The Maven build lifecycle consists of three main lifecycles: Default, Clean, and Site.
     - **Default lifecycle**: Includes phases like `validate`, `compile`, `test`, `package`, `install`, `deploy`.
     - **Clean lifecycle**: Cleans the project by deleting the `target` directory (e.g., `clean`).
     - **Site lifecycle**: Used to generate project documentation (e.g., `site`).

5. **What is the difference between the `install` and `deploy` goals in Maven?**
   - **`install`**: Installs the built artifact (e.g., JAR, WAR) into the local repository (i.e., `~/.m2/repository`), making it available for other projects on the same machine.
   - **`deploy`**: Copies the artifact to a remote repository (e.g., Nexus, Artifactory) for sharing with others.

6. **What is the meaning of a Maven dependency scope (e.g., `compile`, `test`, `provided`)?**
   - **`compile`**: The default scope; dependencies are available in all classpaths.
   - **`test`**: Dependencies used only for testing (e.g., JUnit).
   - **`provided`**: Dependencies provided by the runtime (e.g., Servlet API in a web container).
   - **`runtime`**: Dependencies required at runtime but not at compile time.
   - **`system`**: External dependencies explicitly defined with a system path.

## Intermediate Maven Questions

7. **How does Maven handle transitive dependencies?**
   - Maven automatically resolves transitive dependencies. For example, if your project depends on library `A`, and `A` depends on `B`, Maven will also include `B` in your project's classpath.

8. **What is the difference between `mvn clean` and `mvn clean install`?**
   - **`mvn clean`**: Deletes the `target/` directory where compiled classes and packaged artifacts are stored.
   - **`mvn clean install`**: Cleans the project (deletes the `target/` directory) and installs the built artifact to the local repository.

9. **What is a Maven repository?**
   - A repository is a storage location for project artifacts (e.g., JAR files). There are three types:
     - **Local repository**: Stored on the developer’s machine (`~/.m2/repository`).
     - **Central repository**: A public repository where Maven downloads dependencies from (e.g., Maven Central).
     - **Remote repository**: A private or external repository where companies store their own artifacts.

10. **What is a parent POM in Maven?**
    - A parent POM is a POM file that provides common configurations and dependencies for multiple child projects. It helps manage shared settings like plugin versions, dependency versions, etc., across a set of projects.

11. **What is the Effective POM in Maven?**
    - The Effective POM is the final, combined configuration of a project, including settings from the project’s `pom.xml` and any inherited settings from parent POMs and default Maven configurations. It shows the complete set of resolved configurations for the project.

12. **What are Maven Plugins?**
    - Plugins extend Maven's functionality. They perform specific tasks like compiling code, running tests, or packaging artifacts. Examples include the `maven-compiler-plugin` for compiling code and `maven-surefire-plugin` for running unit tests.

13. **What is a Maven profile, and when would you use it?**
    - A Maven profile is a set of configurations that can be activated in specific environments. You can define multiple profiles for different scenarios (e.g., `development`, `production`) with different dependencies, properties, or plugin configurations.

14. **How can you exclude a transitive dependency in Maven?**
    - You can exclude a transitive dependency in Maven by using the `<exclusion>` tag within a dependency in the `pom.xml` file:
      ```xml
      <dependency>
          <groupId>com.example</groupId>
          <artifactId>library</artifactId>
          <version>1.0.0</version>
          <exclusions>
              <exclusion>
                  <groupId>com.example.transitive</groupId>
                  <artifactId>unwanted-library</artifactId>
              </exclusion>
          </exclusions>
      </dependency>
      ```

## Advanced Maven Questions

15. **What are some common ways to optimize Maven build performance?**
    - Parallel builds using the `-T` option (e.g., `mvn -T 2C clean install`).
    - Using dependency management to avoid redundant dependency resolution.
    - Avoiding the use of SNAPSHOT dependencies.
    - Utilizing incremental builds by skipping unnecessary phases.

16. **How do you resolve version conflicts in Maven dependencies?**
    - Maven resolves version conflicts by using the "nearest-wins" strategy (the closest version in the dependency tree wins). You can also control versions using `<dependencyManagement>` or explicitly specify versions in the `pom.xml`.

17. **What is the use of the `maven-shade-plugin`?**
    - The `maven-shade-plugin` is used to package the application into a single JAR file with all its dependencies included, useful for "uber" or "fat" JARs.

18. **How does Maven handle multi-module projects?**
    - In multi-module projects, a parent POM manages common configurations, and child modules are included as sub-modules. Each module has its own `pom.xml`, but the parent POM aggregates them and provides common configurations.

19. **What is the difference between `mvn clean install` and `mvn clean validate`?**
    - **`mvn clean install`**: Cleans the project and installs the artifact into the local repository.
    - **`mvn clean validate`**: Cleans the project and validates the project configuration, ensuring everything is correct before proceeding with the build.

20. **Can you explain the concept of "Build Profiles" in Maven and how they work?**
    - Build profiles allow you to specify different configurations (like dependencies or plugin settings) based on the environment. Profiles can be activated by specifying a profile name during the build (`mvn -P profileName`), by the operating system, or other properties.

### Troubleshooting and Debugging Questions

21. **How would you troubleshoot a build failure in Maven?**
    - Use `mvn -X` for debug output, review the stack trace, check the dependency tree with `mvn dependency:tree`, and ensure that dependencies are correctly defined.

22. **What is the `mvn dependency:tree` command, and when would you use it?**
    - `mvn dependency:tree` shows the full dependency tree, including transitive dependencies. It is useful for resolving dependency conflicts or identifying why a particular version of a dependency is being used.

23. **What is the purpose of the `mvn validate` command?**
    - The `validate` phase checks if the project is valid, ensuring that all required information and configurations are present before continuing with the build.

24. **How do you add a custom repository in Maven?**
    - You can add a custom repository in the `pom.xml` file within the `<repositories>` tag:
      ```xml
      <repositories>
          <repository>
              <id>my-repo</id>
              <url>https://myrepo.example.com/repo</url>
          </repository>
      </repositories>
      ```

25. **What is the difference between `mvn compile` and `mvn test`?**
    - **`mvn compile`**: Compiles the source code.
    - **`mvn test`**: Runs the tests in the project using the defined test framework (e.g., JUnit).

## Real-World Maven Questions

26. **How do you handle version management in a large team of developers using Maven?**
    - Use `dependencyManagement` in the parent POM to enforce consistent versions across multiple projects. Avoid SNAPSHOT versions in production and ensure that versioning strategies are clearly defined.

27. **Explain the usage of `maven-surefire-plugin` in a test-driven development (TDD) environment.**
    - The `maven-surefire-plugin` is used to run unit tests during the `test` phase. It executes the test classes and generates reports (e.g., in `target/surefire-reports`).

28. **How do you integrate Maven with Jenkins for continuous integration?**
    - Jenkins can be configured to run Maven builds automatically. You can define a Maven build step in Jenkins to execute the `mvn clean install` command and monitor the results.

29. **Can you explain the purpose of the `maven-assembly-plugin`?**
    - The `maven-assembly-plugin` is used to create custom distributions of your project, such as bundled JARs with dependencies or ZIP files.

30. **How do you ensure reproducible builds in Maven?**
    - Ensure you use fixed versions for all dependencies (no SNAPSHOTs), use the `<dependencyManagement>` section to manage versions, and ensure the build environment is consistent across teams.
