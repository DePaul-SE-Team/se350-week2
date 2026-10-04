# Structural Testing – IntelliJ & JaCoCo Setup

## Background

In this tutorial, you will learn how to use code coverage tools and analyze the results. Coverage measures how much code is executed when tests run. Coverage tools are commonly integrated into the build or CI process to help assess software quality.

This tutorial has two parts:

1. Measure coverage using IntelliJ IDEA.
2. Use JaCoCo, a third-party library.

## Part 1 – IntelliJ Coverage Setup

### 1. Run with coverage

In IntelliJ, right-click a test class or method and choose **Run with Coverage**. A coverage report window will appear; click **Run with Coverage**.

### 2. Read the report

The coverage tool shows **Line %** and **Branch %**:

- **Line coverage:** Percentage of individual lines executed by the tests. A value of 100% means every counted line ran at least once.
- **Branch coverage:** Percentage of decision outcomes executed. A value of 83% means some decision paths were not exercised.

Line coverage records whether a line ran. Branch coverage checks decision outcomes, such as the true and false outcomes of an `if` condition.

### 3. Inspect coverage coloring in source

Open `CountWords.java` and look at the highlighting in the gutter:

| Color | Meaning |
| --- | --- |
| Green | Fully covered line |
| Yellow | Partially covered line, such as a decision with only one outcome tested |
| Red | Line never executed |
| No color | Structural line, such as `}`, that is not counted |

Hover over a yellow line to see hit counts. For example, **true hits: 2** means the condition evaluated to true twice, and **false hits: 14** means it evaluated to false fourteen times.

IntelliJ provides a convenient view of coverage. This tutorial also configures JaCoCo directly for Maven-based reporting and CI.

### 4. Compare line and branch coverage

- **Line coverage:** Did this line run at least once?
- **Branch coverage:** Did we exercise both true and false outcomes?

For example:

```java
if (x < 3) { ... }
```

Branch coverage requires tests for both `x < 3` being true and false.

### 5. Discussion

The IDE report is convenient for quick analysis. For automation and CI pipelines, configure JaCoCo directly in Maven.

## Part 2 – JaCoCo Coverage Setup

JaCoCo is a free, open-source Java coverage tool. It reports lines, branches, methods, and cyclomatic complexity; integrates with Maven, Gradle, Ant, Jenkins, and SonarQube; and produces HTML, XML, and CSV reports.

A JaCoCo report shows covered and missed instructions, branches, lines, methods, and classes. Other coverage tools mentioned in the source are OpenClover, Cobertura, and Emma.

### Step 1 – Configure JaCoCo in Maven

**A. Declare the version** in `pom.xml`:

```xml
<properties>
  <jacoco.version>NEW VERSION</jacoco.version>
</properties>
```

Replace `NEW VERSION` with the JaCoCo version selected for your project.

**B. Add the plugin** inside `<build><plugins>`:

```xml
<plugin>
  <groupId>org.jacoco</groupId>
  <artifactId>jacoco-maven-plugin</artifactId>
  <version>${jacoco.version}</version>
  <executions>
    <!-- Section A: attach agent before tests -->
    <execution>
      <id>prepare-agent</id>
      <goals>
        <goal>prepare-agent</goal>
      </goals>
    </execution>
    <!-- Section B: generate report after tests -->
    <execution>
      <id>report</id>
      <phase>test</phase>
      <goals>
        <goal>report</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

- **`prepare-agent`:** Instruments code at runtime to collect coverage during tests.
- **`report`:** Reads the coverage data after tests and generates reports.

If you get zero test run please add `mavens surefire`

```xml
   <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.6.0</version>
        <dependencies>
            <dependency>
                <groupId>org.junit.jupiter</groupId>
                <artifactId>junit-jupiter-engine</artifactId>
                <version>6.0.3</version>
            </dependency>
        </dependencies>
    </plugin>
```

### Step 2 – Run tests with JaCoCo

```bash
mvn clean test
```

Then open `target/site/jacoco/index.html` in a browser. Green bars indicate covered code, red bars indicate missed code, and diamonds mark branching decisions such as `if`, `for`, `while`, `?:`, `switch`, and lambdas. Hover over them to inspect outcomes.

### Step 3 – Understand JaCoCo reports

- **Instructions:** Bytecode instructions executed.
- **Lines:** Source lines executed.
- **Branches:** Decision outcomes exercised.
- **Methods and classes:** Coverage aggregated by scope.
- **Cyclomatic complexity:** A measure related to the number of independent paths.

## Part 4 – Achieve 100% Coverage

Add a branch to the starter code, such as an `if`/`else`, and write tests that increase branch coverage from below 100% to 100%.

