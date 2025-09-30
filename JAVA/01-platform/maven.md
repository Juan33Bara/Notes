# MAVEN

## COMPLETE COMMANDS AND CODE TO CREATE A MAVEN PROJECT (SUMMARY)

### First step

- Run this code to create an archetype generic maven project
    ```bash
    # Git Bash
    mvn archetype:generate -DgroupId=ar.edu.utnfc.backend \
    -DartifactId=proyect-name \
    -DarchetypeGroupId=org.apache.maven.archetypes \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
    ```
- This command creates a structure like this:
    ```plaintext
    proyect-name/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   │   └── ar/edu/utnfrc/backend/App.java
    │   │   └── resources/
    │   └── test/
    │       ├── java/
    │       │   └── ar/edu/utnfrc/backend/AppTest.java
    │       └── resources/
    └── pom.xml
    ```

### Second step

- Use the command **mvn compile**
- If all goes well, maven will create a **target/** directory with the compiled classes

### Third step

- To package the project as a JAR, you need to add a plugin to the **pom.xml** file
- **Be careful**, when you create an archetype, add a basic plugin with the **maven-compiler-plugin** to specify the
  java
  version. So remove it or replace it with the below code
- Add this code inside the **plugins** tags:
    ```xml
    <plugin>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.4.2</version>
        <configuration>
            <archive>
                <manifest>
                    <mainClass>ar.edu.utnfc.backend.App</mainClass> // Specify the main class here, the complete package path (from java)
                </manifest>
            </archive>
        </configuration>
    </plugin>
    ```
- Then, you can execute the command **mvn package** to create the JAR file
- The JAR file will be created in the **target/** directory
- The file is like this **proyect-name-1.0-SNAPSHOT.jar**
- You can execute using **java -jar** but we are gonna use a plugin to make it easier

### Fourth step

- If you want to use the command **mvn exec:java** to run the project, you need to add this plugin to the **pom.xml**
  file
- Add this code inside the **plugins** tags:
    ```xml
    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.1.0</version>
        <configuration>
            <mainClass>ar.edu.utnfc.backend.App</mainClass> // Specify the main class here, the complete package path (from java)
        </configuration>
    </plugin>
    ```
- After adding this plugin, you can use the command **mvn exec:java** to run the project

### Fifth step (The complete command)

- If you want, you can write a command to do all the steps in one command
- You can use this command:
    ```bash
    mvn clean compile exec:java
    ```

### Sixth step (To execute other main classes)

- We are gonna use this to execute other main classes
- You need to comment a part of the exec plugin in the **pom.xml** file
    ```xml
    <!-- <configuration>
        <mainClass>ar.edu.utnfc.backend.App</mainClass> 
    </configuration> -->
    ```
- Then, you can use this command to execute any main class
    ```bash
    mvn clean compile exec:java -Dexec.mainClass="ar.edu.utnfrc.backend.OtherMainClass"
    ```
- To execute the main class **App.java**, you can use this command
    ```bash
    mvn clean compile exec:java -Dexec.mainClass="ar.edu.utnfrc.backend.App"
    ```

## Maven Overview

- Maven is a powerful tool for building and managing Java projects.
- It simplifies project setup, dependency management, and automates the build lifecycle.
- Maven can be seen from three main perspectives:
    - Project Structure Generator
    - Dependency Management
    - Build Lifecycle Management

### Project Structure Generator

- Maven uses archetypes (**templates**) to create standardized project structures.
- Each project includes a **pom.xml** (Project Object Model) file, **source directories** (src/main/java, src/test/java)
  and
  allows consistent organization.
- **Basic structure**
    - The basic structure of a Maven project in Java follows a standard convention.
    - Here is an example of the directory structure:
    ```plaintext
    hola-mundo/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   └── resources/
    │   └── test/
    │       ├── java/
    │       └── resources/
    └── pom.xml
    ```  
    - Where:
        - **src/main/java:** Contains the main application source code.
        - **src/main/resources:** Contains resources (configuration files, property files, etc.) used by the main
          application.
        - **src/test/java:** Contains unit and integration tests.
        - **src/test/resources:** Contains resources used by the tests.

- **Key identifiers when creating a project:**
    - **GroupId** → project group (usually reversed domain, e.g., com.example or ar.edu.utnfrc.backend)
    - **ArtifactId** → project name (e.g., hello-world)
    - **Version** → version of the artifact (e.g, 1.0-SNAPSHOT for development).
        - SNAPSHOT: Indicates a development version that may change frequently.
        - RELEASE: Indicates a stable version that is ready for production.
    - **Artifact:**
        - An artifact is a file or collection of files produced by a build process, such as a JAR, WAR, or EAR file.
            - JAR (Java ARchive): packaged Java classes and resources, used for libraries or applications.
            - WAR (Web Application Archive): packaged web applications, including servlets, JSPs, and static resources.
            - EAR (Enterprise Archive): packaged enterprise applications, can include JARs, WARs, and configuration
              files
              for deployment.
              ![img.png](Images/artefacts.png)
        - It is the **compilation unit** or indivisible component within the Java infrastructure and receives an
          identifier
          that, together with the **GroupId** and **Version**, must be unique.
        - Essentially, an artifact is **associated** with a **Maven project** and is the **resulting** product of
          building
          it (e.g., a JAR, WAR, or EAR).
        - The project that generates it consists of a **container directory** that includes the
          **pom.xml** file and the standard project directory and file structure.
        ```go
        Maven Project --> mvn package --> Artifact (JAR/WAR/EAR)
        ```

### Dependency Management

- **Dependency concept:**
    - A dependency is an external library, API, or module used by a project to perform specific functions.
    - Dependencies allow code reuse and prevent reinventing functionality.
    - Proper management is essential, because uncontrolled dependencies can lead to conflicts or errors.
- Maven manages dependencies declared in the **pom.xml** using the **<dependency>** tag.
- Each **<dependency>** specifies: **groupId**, **artifactId**, and **version** of the library.

#### Key Characteristics:

- **Declarative Declaration** → declare dependencies in pom.xml, Maven handles everything automatically.
- **Automatic Resolution** → resolves transitive dependencies required by other libraries.
- **Central and Remote Repositories** → downloads dependencies from trusted sources like Maven Central.
- **Local Repository (.m2)** → stores downloaded libraries locally to avoid repeated downloads and enable offline
  development.

### Build Lifecycle Management

- Maven follows a standard build lifecycle with **different phases**, each responsible for a specific task in the
  development and build process.
- Some key phases of the build lifecycle are:
    - **clean**: Deletes all files generated by previous builds, leaving the project clean to start fresh.
    - **validate**: Checks that the project is correct and that all required dependencies are available.
    - **compile**: Compiles the project’s source code.
    - **test**: Runs automated tests.
    - **package**: Packages the compiled code into an artifact (such as a JAR or WAR).
        - If its a JAR, it will be created in the **target/** directory.
        - In the pom.xml, its specified the entry point of the JAR, which is the main class that will be
          executed when running the JAR.
    - **install**: Installs the artifact into the local repository for use by other projects.
    - **deploy**: Copies the final artifact to a remote repository to share it with other developers.
      ![img.png](Images/lifecycle.png)

#### Maven build lifecycle phases

| Phase    | Description                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| validate | Checks that the project is well-formed and all necessary information is valid.               |
| compile  | Compiles the project’s source code.                                                          |
| test     | Runs unit tests using a testing framework like JUnit.                                        |
| package  | Packages the compiled code into a distributable format, such as a `.jar` or `.war`.          |
| verify   | Performs any checks on the packaged artifact to ensure quality and correctness.              |
| install  | Installs the artifact into the local repository (`.m2`) so it can be used by other projects. |
| deploy   | Copies the final artifact to a remote repository to share it with other developers.          |

### pom.xml file

- In addition to the directories of a Maven project, the project includes the **pom.xml** file, which we’ve mentioned
  previously.
- This file is **central to a Maven project**.
- It is a **text file in XML** (Extensible Markup Language) format that contains the **project configuration.**
- With the project directory, source files, and pom.xml, the **project can be opened and worked on in any IDE that
  supports Maven projects.**
- Here are the key elements of a pom.xml with explanations:

```xml

<project>
    <!-- Maven project model version -->
    <modelVersion>4.0.0</modelVersion>

    <!-- Project group identifier (usually reversed domain of the organization) -->
    <groupId>ar.edu.utnfc.backend</groupId>

    <!-- Project artifact identifier (unique project name) -->
    <artifactId>hola-mundo</artifactId>

    <!-- Project version -->
    <version>1.0.0-SNAPSHOT</version>

    <!-- Descriptive project name -->
    <name>Hola Mundo Maven</name>

    <!-- Short project description -->
    <description>A simple Maven project</description>

    <!-- Properties for the project -->
    <properties>
        <!-- Java version to use for compilation -->
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

    <!-- Project dependencies -->
    <dependencies>
        <!-- List your project dependencies here -->
        <!-- Example dependency on JUnit for testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope> <!-- Scope indicates this dependency is only needed for testing -->
        </dependency>
    </dependencies>

    <!-- Build configuration -->
    <build>
        <!-- Plugins used during the build -->
        <plugins>
            <!-- Maven Compiler Plugin configuration -->
            <plugin>
                <!-- Plugin group ID -->
                <groupId>org.apache.maven.plugins</groupId>

                <!-- Plugin artifact ID -->
                <artifactId>maven-compiler-plugin</artifactId>

                <!-- Plugin version -->
                <version>3.8.1</version>

                <!-- Plugin-specific configuration -->
                <configuration>
                    <!-- Set source and target Java versions using properties -->
                    <source>${maven.compiler.source}</source>
                    <target>${maven.compiler.target}</target>
                </configuration>
            </plugin>
            <!-- Add other build plugins here if needed -->
        </plugins>
    </build>
</project>

```

- **Dependencies:** These are libraries, APIs, or modules that the project requires to function correctly.
    - Each dependency is defined with a **groupId**, **artifactId**, and **version**.
    - The **scope** of a dependency indicates where it is used (e.g., compile, test, runtime).
- **Plugins:** These are tools that extend Maven's functionality, allowing you to perform tasks like compiling code,
  running tests, packaging artifacts, and more. These tools are used by Maven while building the project.
    - Each plugin is defined with a **groupId**, **artifactId**, and **version**.
    - Plugins can have specific configurations, such as setting the Java version for compilation.

### Location of the .m2 Directory

- Installing Maven includes a special directory called **.m2**.
- The **.m2 directory** serves as the **local repository** and its location is the same across different operating
  systems.
- By default, it is located in the user’s home directory:
    - Windows: **C:\Users\YourUsername\.m2**
    - Linux / macOS: **/home/YourUsername/.m2**
- If you need to add any **specific or custom configuration for Maven**, you can do so in a file named **settings.xml**
  located directly inside the .m2 folder.
- However, **Maven works perfectly fine without this file, using its default configuration.**

## MAVEN Installation and Setup

### 1️⃣ Download & Install**

- Download ZIP: https://maven.apache.org/download.cgi
- Extract to: **C:\Herramientas\apache-maven-3.9.6**
- (Optional) Rename folder: **C:\Herramientas\maven**

### 2️⃣ Set Environment Variables

- **MAVEN_HOME** → `C:\Herramientas\maven`
- Add to **Path** → `%MAVEN_HOME%\bin`
- **Git Bash**: add at the end of this file `~/.bashrc`, with **nano** or your favorite editor
    ```bash
      export MAVEN_HOME="/c/Herramientas/maven"
      export PATH="$MAVEN_HOME/bin:$PATH"
      source ~/.bashrc
    ```

### 3️⃣ Verify Installation

- ✅ Should show Maven version, home path, and Java version.
    ```bash
    mvn -v
    which mvn   # optional
    ```

## MAVEN project setup and commands to compile, package, and run

- You can create a project using the command line or from the IDE.

### Create a New Maven Project Generic from the IDE IntelliJ IDEA

1. Create a container folder
    - Make a folder outside IntelliJ, e.g.: `BACK/`
    - **Do not open this folder directly in IntelliJ**, or it will convert it into a single project.

2. Create Maven projects inside the container
    - In IntelliJ: **File** → **New** → **Project** → **Maven**
    - Choose **GroupId**, **ArtifactId** and set the project location inside **BACK/**
    - IntelliJ creates the basic Maven structure:
        ```swift
        ProyectoMaven/
        ├─ src/ASasaSasAASSas
        │  ├─ main/
        │  │  └─ java/
        │  │     └─ (your packages and classes here)
        │  └─ test/
        │     └─ java/
        │        └─ (your test packages and classes here)
        ├─ pom.xmlasASa by week or microservice
    - Each week or microservice gets its own Maven project inside BACK:
    ```swift
        BACK/
        ├── week1-project/
        ├── week2-project/
        ├── week3-project/
        └── week4-project/
    ```
    - Add **packages** for activities inside **src/main/java** as needed.
4. Version control
    - Only commit **src/** and **pom.xml**
    - **.idea/** and **.iml** can be ignored.

### Create a New Maven Project Generic from the Command Line (Hello Wold project)

- Before, we create a project without use Maven as a manager, then we compile and run it manually.
- Now, we will use Maven to create the project and handle all the build and execution tasks for this software artifact.

1. Creating the Project

- We will create the project using a Maven archetype.
- Maven Central provides a predefined archetype for creating a basic Java application called:
  `maven-archetype-quickstart`.
- To create the project, run the following command :
    ```cmd
    // CMD
    mvn archetype:generate "-DgroupId=ar.edu.utnfc.backend" `
    "-DartifactId=hola-mundo" `
    "-DarchetypeGroupId=org.apache.maven.archetypes" `
    "-DarchetypeArtifactId=maven-archetype-quickstart" `
    "-DinteractiveMode=false"
    ```
    - **Note:** In PowerShell, each argument must be enclosed in **double quotes**; otherwise, Maven will produce an
      error.
      ```bash
      # Git Bash
      mvn archetype:generate -DgroupId=ar.edu.utnfc.backend \
      -DartifactId=hola-mundo \
      -DarchetypeGroupId=org.apache.maven.archetypes \
      -DarchetypeArtifactId=maven-archetype-quickstart \
      -DinteractiveMode=false
      ```
- If everything works correctly, Maven will generate the project.
- You can also use the interactive mode, which will prompt you for each parameter.
- In this case, you can run the command without the `-DinteractiveMode=false` option:
    ```bash
    mvn archetype:generate -DgroupId=ar.edu.utnfc.backend -DartifactId=hola-mundo
    ```

2. Reviewing the Project Created by Maven

- Inside the project directory **(hola-mundo)**, you will find the following structure:
    ```plaintext
    hola-mundo/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   └── resources/
    │   └── test/
    │       ├── java/
    │       └── resources/
    ├── pom.xml
    └── site/
    ```
- Key elements to note:
    - **pom.xml:** The core configuration file of the Maven project.
    - **src directory:** Contains the main source code and test code.
    - **site directory:** Used by the Maven site plugin to generate project documentation (not used for backend projects
      here).
    - **App.java:** Located in **main/java/<packages based on groupId>/**, this file contains a simple "Hello World"
      program.

**- PACKAGE:** Packages in Java are directories that organize classes and correspond to the package statement at the top
of each .java file.

- Finally, **the heart of the Maven project is the pom.xml**, which defines project settings, Java version (default 1.7,
  changed here to 17), JUnit dependency for unit testing, and build plugins.

3. Building the Hello World Project

- Open the project in IntelliJ or use your system terminal.
- Inside the project directory, run:
    ```bash
    mvn compile
    ```
- If successful, Maven will create a **target** directory containing **compiled classes.**
- For example:
    ````plaintext
    hola-mundo/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   └── resources/
    │   └── test/
    │       ├── java/
    │       └── resources/
    ├── pom.xml
    ├── site/
    └── target/
        ├── classes/
        │   └── ar/
        │       └── edu/
        │           └── utnfc/
        │               └── backend/
        │                   └── App.class
        ├── test-classes/        <- In a simple archetype, this may be empty
        │   └── ar/
        │       └── edu/
        │           └── utnfc/
        │               └── backend/
        │                   └── AppTest.class
        └── generated-sources/
    
    ````

#### Packaging the Application as an Executable JAR

- We can run with `java App`, but it is more elegant to package the application as an executable JAR.
    - You need to be in the project root directory
    - Execute the following command:
    ```bash
    java -cp target/classes ar.edu.utnfc.backend.clase1.HelloWorld
    ```
    - cp: classpath, which is the path where Java will look for classes to execute.
- To run the application more elegantly, we need to configure the **JAR plugin** in **pom.xml** to specify the **main
  class**, which tells Maven which class contains the **main method**:
    ```xml
    <plugin>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.0.2</version>
        <configuration>
            <archive>
                <manifest>
                    <mainClass>ar.edu.utnfc.backend.App</mainClass> // Specify the main class here, the complete package path (from java)
                </manifest>
            </archive>
        </configuration>
    </plugin>
    ```
- Then, build the project with:
    ```bash
    mvn package
    ```
- After this, the **target** directory will contain the executable **JAR file**:
  `hola-mundo-1.0-SNAPSHOT.jar`
- Inside the JAR, the **MANIFEST.MF** file specifies the main class to be executed.
  ![img.png](Images/manifest.png)

4. Running the Application

- Now we have an **executable Java component**.
- Java itself cannot generate a standalone executable; instead, it creates
  .**class files packaged into a JAR** (Java Archive) containing everything needed to run the application.
- To execute the **JAR**, use the **Java Virtual Machine** with the **-jar flag**:
    ```bash
    java -jar target/hola-mundo-1.0-SNAPSHOT.jar
    ```
- And there it is — your **Hello World application** running successfully.

#### Alternative Execution Using Maven (mvn exec:java)

##### Why and How You Can Run Java with Maven**

- Maven as a Task Orchestrator
- Maven **is not a compiler or interpreter**.
- It is a **build automation framework** for Java (and other languages, though mainly Java).
- **Maven itself does not perform compilation or execution**; **it relies on plugins**, which are **specialized
  components
  capable of performing specific tasks:** compiling, testing, packaging, etc.
- For example:`mvn compile`
    - **Maven does not directly call javac.**
    - It **invokes** the `maven-compiler-plugin`, which **handles compilation according to its configuration.**
- Similarly, to execute a Java program, you can use: `mvn exec:java`
    - This command **does not directly call java.**
    - It **invokes** the `exec-maven-plugin`, which runs Java with the configured main class and classpath.

##### Configuring exec-maven-plugin in pom.xml

- To use `mvn exec:java`, add this to your `<build><plugins>` section:
    ```xml
    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.1.0</version>
        <configuration>
            <mainClass>ar.edu.utnfc.backend.App</mainClass>
        </configuration>
    </plugin>
    ```
- `mainClass` points to the class with the **main** method to execute.

**To execute other class (not the main set)**

- Example of package path: `ar.edu.utnfc.backend.clase1.HelloWorld`
- Command to run:
    ```bash
    mvn exec:java -Dexec.mainClass="ar.edu.utnfc.backend.clase1.HelloWorld"
    ```
    - This **overwrites** the **App class** you put in the plugin.
    - Maven takes care of using the correct **classpath**, with all dependencies if there are any.

##### Advantages of Using mvn exec:java

1. Classpath Automatically Managed

- Maven resolves all dependencies and sets up the classpath correctly.
- No need to manually build or write the classpath.

2. Integrated with Maven Lifecycle

- You can run:
    ```bash
    mvn clean compile exec:java
    ```
- This ensures a fresh build and reliable execution, which is crucial for larger projects.

3. Works for Simple or Complex Projects

- Even advanced frameworks like **Spring Boot** use Maven plugins (`spring-boot:run`) that do the same: resolve
  dependencies, set classpath, and execute.

##### When and Why to Use mvn exec:java

- During development for **small applications**, avoiding the need to package **.jar** files.
- For scripts executed in CI/CD pipelines without packaging.
- For educational or testing projects, reducing friction with manual terminal commands.
- Ensures consistency with the entire Maven lifecycle: dependency resolution, compilation, and plugin executionto rely

### The internal process when you click "run" in the IDE

- When you click "run" in the IDE, it does not directly execute the Java class.
- Instead, it uses the **Maven build lifecycle** to compile and run the project.
- The IDE internally runs the following commands:
    ```bash
    mvn clean compile exec:java -Dexec.mainClass="ar.edu.utnfc.backend.App"
    ```
- This ensures that the project is cleaned, compiled, and executed with the correct classpath and dependencies.
- So, basically, do the entire process of building and running the project, **just like you would do manually in the
  terminal**.

## How im gonna organize the packages

### 📂 Proposed Structure Inside a Maven Project

- If your **groupId** is **com.exercises**, your project would look like this:
    ```plaintext
    project/
    │
    ├── pom.xml
    │
    └── src/
        └── main/
            └── java/
                └── com/
                    └── exercises/
                        ├── week1/
                        │   ├── class1/
                        │   │   ├── Activity1.java
                        │   │   ├── Activity2.java
                        │   │   └── ...
                        │   ├── class2/
                        │   │   ├── Activity1.java
                        │   │   └── ...
                        │   └── ...
                        │
                        ├── week2/
                        │   ├── class1/
                        │   │   ├── Activity1.java
                        │   │   └── ...
                        │   └── ...
                        │
                        ├── week3/
                        │   └── ...
                        │
                        └── app/
                            └── App.java   ← Entry point for a final single project
    
    ```

#### 💡 Concept

**During learning/practice:**

- Each **activity** is an independent script with its own `main`.
- You can have many `.java` files without dependencies between them.
- Execution is independent: you choose which file to run in your IDE or terminal.

**When building a single application:**

- Only one `main` in `App.java` (inside `/app`).
- All other code are classes/methods called from App.
- The project runs from a single entry point.

### 📜 Instructions for Independent Scripts (Maven)

1️⃣ Create the file

- Example: `src/main/java/com/exercises/week1/class1/Activity1.java`
- 2️⃣ Sample code
    ```java
    package com.exercises.week1.class1;
    
    public class Activity1 {
      public static void main(String[] args) {
          System.out.println("Hello from Activity 1");
      }
    }
    ```
- 📌 Important Note:
    - The `package` **must match** the folder path after `java/`.
    - Example:
        - Folder → `/com/exercises/week1/class1`
        - Package → `package com.exercises.week1.class1;`

### ⚙️ How to Run in Maven

- IDE (IntelliJ / Eclipse): Right-click the class → Run 'Activity1.main()'
- Console (from Maven project root):
    ```bash
    mvn compile
    mvn exec:java -Dexec.mainClass="com.exercises.week1.class1.Activity1"
    ```

### 📜 Instructions for a Single Application

- When you want to combine everything into one app:
    - Place App.java in: `src/main/java/com/exercises/app/App.java`
- Example:
    ```java
    package com.exercises.app;
    
    import com.exercises.week1.class1.Activity1;
    import com.exercises.week1.class2.Activity2;
    
    public class App {
      public static void main(String[] args) {
          Activity1.run(); // Call method from Activity1
          Activity2.run(); // Call method from Activity2
      }
    }
    ```
- Run:
    ```bash
    mvn compile
    mvn exec:java -Dexec.mainClass="com.exercises.app.App"
    ```

**⚖️ Key Difference**

| Mode                    | Main in each class | Single Main |
|-------------------------|--------------------|-------------|
| **Independent scripts** | ✅ Yes              | ❌ No        |
| **Final app**           | ❌ No               | ✅ Yes       |

## Repositories

- it’s important to briefly explain the concept of a **repository** and the different types of repositories Maven
  interacts
  with during the project lifecycle.

### Maven relies on several types of repositories:

#### Central Repository:

- The **Maven Central Repository** is a **globally** maintained repository by the Maven community.
- It is the **default repository from which Maven downloads dependencies** declared in your **pom.xml**.
- Central **hosts a vast collection of commonly used Java libraries and artifacts**, making it easy to include
  dependencies in your projects without manually downloading them.

#### Remote Repositories:

- A remote repository is a **server that stores project dependencies and artifacts.**
- You can **configure Maven** to use **additional remote repositories besides Central.**
- This is **useful when working with specific libraries or in environments** with network restrictions.
- **Maven downloads dependencies from these remote repositories** as needed and caches them locally for reuse.
- Access to remote repositories **can be configured** either in the **pom.xml** for a specific project or in the *
  *settings.xml**
  for all projects on your machine.

#### Local Repository / Cache:

- The local repository is a **directory on your system** where **Maven stores downloaded dependencies.**
    - Like **node_modules** in Node.js
- By default, this is the `.m2` folder in your user directory.
- When Maven downloads a dependency for the first time from a remote repository, it **stores it locally.**
- This **avoids repeated downloads** in the future and allows projects to be built offline.

### Local .m2 Folder: Local Repository vs. Remote Dependency Cache

- The `.m2` directory serves **both** as a **local** **repository** and a **cache** for remote dependencies.
- Here’s a breakdown:

#### Local Repository (.m2):

- Stores **all dependencies downloaded on your system.**
- **Prevents repeated downloads** by allowing Maven to reuse already downloaded dependencies.
- Facilitates building projects **offline** by providing previously downloaded dependencies.
- **Supports team collaboration** by letting all team members use the same locally stored dependencies.

#### Remote Dependency Cache:

- Acts as a **temporary cache for dependencies downloaded** **from remote repositories.**
- **Maven first checks this cache before attempting to download a dependency again.**
- Improves performance by reducing repeated downloads from remote repositories.

## 🧩 Annex 1: Including Dependencies in a JAR (Fat JAR / Uber JAR)

- By default, **Maven generates a JAR containing only the project’s own classes.**
- If your application uses external libraries (like JUnit, Gson, etc.), running it with `java -jar` **may fail due to
  missing classes.**
- To solve this, you can create a **Fat JAR** or **Uber JAR**, which **includes all dependencies**, using the
  `maven-assembly-plugin.`

### Key points

#### Fat/Uber JAR contains:

- Your compiled classes (`src/main/java`)
- Project resources (`src/main/resources`)
- All **external dependencies downloaded by Maven**

#### Effect:

- Produces a single, self-contained executable JAR that **runs anywhere** with Java, without needing additional
  libraries or
  classpath configuration.

### Maven behavior

#### Default mvn package

- Compiles your code
- Packages it in `target/project-1.0.jar`
- **Does not include dependencies** → may fail if external libraries are used

#### With maven-assembly-plugin:

- Combines your code and all dependencies into one JAR
- Adds a proper `META-INF/MANIFEST.MF` with `Main-Class` entry
- Produces `target/project-1.0-jar-with-dependencies.jar`
- Can be executed with:
    ```bash
    java -jar target/project-1.0-jar-with-dependencies.jar
    ```

### Why use an Uber JAR?

- Run your app on any machine without Maven installed
- Deploy simple apps (CLI tools, microservices, batch tasks) easily
- Avoid classpath conflicts in complex environments
- Understand how a real Java application manages classes, dependencies, and execution

### Technical note:

- Internally, a JAR is a ZIP with classes and a manifest.
- Maven merges all compiled classes and dependency contents into one JAR and ensures a valid manifest.

### Bottom line:

- For small projects, it’s optional, but for projects with dependencies, an Uber JAR ensures portability, ease of
  execution, and reliability.

### Code of the plugin to add in the pom.xml

```xml

<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>3.3.0</version>
    <configuration>
        <archive>
            <manifest>
                <mainClass>ar.edu.utnfc.backend.App</mainClass>
            </manifest>
        </archive>
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
```

## 🚀 What’s Next? Introduction to mvn deploy and Remote Repositories

- So far, we have seen how to use Maven to **compile, test, and package** a project locally.
- But what happens when **we need to share that artifact** (.jar) with other teams or projects?
- This is where the **deploy** step comes in.

### What is mvn deploy?

- The mvn deploy command is the **final step in Maven’s build lifecycle.**
- It is used to **upload (deploy) the generated artifact** to a **remote repository**, from which other projects can
  download it as a dependency.
- Command:
    ```bash
    mvn deploy
    ```
- This **only makes sense when a remote repository is configured and accessible to Maven** (for example, a private
  server within your organization).

### What is a Remote Repository?

- A **Maven remote repository** is a specialized server that **stores Java artifacts** (such as .jar, .war, .pom, etc.)
  and organizes them by:
    - groupId
    - artifactId
    - version
- Maven projects can **publish** **artifacts** to these repositories and **consume artifacts** from them as
  dependencies.

### Popular Software for Remote Repositories

- Nexus Repository Manager (Sonatype)
    - Widely used in companies, free OSS version available.
- JFrog Artifactory
    - Professional, feature-rich, with a free version.
- Apache Archiva
    - Simpler open-source alternative.
- GitLab Package Registry
    - Allows uploading .jar artifacts to GitLab projects, integrating dependency management with version control and
      CI/CD. Compatible with Maven through pom.xml and settings.xml configuration.

### How to Use deploy

- To deploy your .jar to a remote repository, you need:

1. A pom.xml that contains information about the remote server (<distributionManagement>).
2. Credentials configured in ~/.m2/settings.xml.
3. A running server like Nexus or Artifactory.
4. Execute:
    ```bash
    mvn deploy
    ```

- Maven will package and upload your artifact to the remote server, along with its pom.xml and metadata.
