## Maven BOM
    A Maven Bill of Materials (BOM) is a specialized Maven Project Object Model (POM) file
    designed to manage dependency versions within a project or across multiple related projects.

    It does not load any dependencies itself.

    It only provides version information for those dependencies.

    A example:
```
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.7.5</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

## Maven <parent> (Inheritance)
    The `<parent>` element enables POM inheritance. It specifies that the current project
    inherits configuration from a parent project. This allows for sharing common settings,
    dependencies, and plugins across multiple projects.

    A example:
```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.5</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```
    To share dependencies management with child projects,
    you can use the `<dependencyManagement>` in parent POM along with `<parent>` in child POMs.

    An example:
```
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.7.5</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

    To share plugins management with child projects,
    you can use the `<pluginManagement>` in parent POM along with `<parent>` in child POMs. 
    An example: in parent POM:
```
    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                    <version>2.7.5</version>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
```
    And in child POM:
```
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

## Multi-Module Maven Project (Aggregation)
    A multi-module Maven project is a project structure that consists of a parent project
    and multiple sub-modules (child projects).

    The child's pom.xml may use the `<parent>` element to point to its containing parent POM,
    or it can points to another project's POM to inherit from. So 'parent' could mean
    either the aggregator project or another project.

    An example of a multi-module Maven project structure:
```
    my-multi-module-project/
    ├── pom.xml (Parent POM)
    ├── module-a/
    │   └── pom.xml (Sub-module A POM)
    ├── module-b/
    │   └── pom.xml (Sub-module B POM)
    └── module-c/
        └── pom.xml (Sub-module C POM)
```

    In the parent `pom.xml`, you would define the modules like this:
```
    <modules>
        <module>module-a</module>
        <module>module-b</module>
        <module>module-c</module>
    </modules>
```

    Each sub-module's `pom.xml` would specify its own dependencies and configurations,
    while inheriting common settings from the parent POM.