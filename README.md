<p align="center">
<a href="https://github.com/guilhermemarimzup/dependency-vuln-checker">
  <img src="./images/owl.png" width="250" />
</a>

<h1 align="center">Owldency - Vulnerable Dependencies Hunter</h1>

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Owldency is a GitHub action that checks if your application uses dependencies with known vulnerabilities. Actually it supports applications that use [Maven](https://maven.apache.org/), [Gradle](https://gradle.org/), and [npm](https://www.npmjs.com/) as the package manager. Under the hood, it uses [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/) and [npm audit](https://docs.npmjs.com/cli/v7/commands/npm-audit) to check the dependencies.


Finishing the analysis, Owldency will generate an artifact that has a HTML file containing the results. For applications that use Maven or Gradle, the HTML file will be generated by [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/), and for applications that use npm, it will be generated by [npm-audit-html](https://www.npmjs.com/package/npm-audit-html) plugin.



---

<h2>
    <img src="./images/usage.svg" alt="Usage icon" width="25px"/> Usage
</h2>

The simplest way to add Owldency in your workflow is just adding it as a step of your current workflow.

```yaml
- name: Owldency
  uses: guilhermemarimzup/owldency@v1
```

<h3>
    <img src="./images/pre-requisites.svg" alt="Pre-requisites icon" width="25px"/> Pre-requisites
</h3>

If you are using [Maven](https://maven.apache.org/) or [Gradle](https://gradle.org/) as your package manager, you must add the [OWASP dependency-check plugin](https://jeremylong.github.io/DependencyCheck/modules.html) in your dependency manager file because the results will be much more accurate. If you're using [npm](https://www.npmjs.com/), you can skip this section.

#### Maven Plugin Example - `pom.xml`

```xml
<plugin>
    <groupId>org.owasp</groupId>
    <artifactId>dependency-check-maven</artifactId>
    <version>6.1.2</version>
    <configuration>
        <formats>
            <format>HTML</format>
            <format>JSON</format>
        </formats>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

#### Gradle Plugin Example - `build.gradle`

```gradle
plugins {
	id 'org.owasp.dependencycheck' version '6.1.2'
}

dependencyCheck {
    formats = ['HTML', 'JSON']
}
```

Take care with your `.gitignore` file, because this action needs `gradlew` file to execute dependency-check plugin, if your `.gitignore` file is ignoring `gradle-wrapper.jar` and `gradle-wrapper.properties`, this action will not run as expected.

---

<h2>
    <img src="./images/github-actions-logo.svg" alt="GitHub Actions icon" width="25px"/> Workflow Example
</h2>
 

```yaml
name: Owldency

on: push

jobs:
  owldency:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Owldency
      uses: guilhermemarimzup/owldency@v1
```

---

<h2>
    <img src="./images/licenses.svg" alt="Licenses icon" width="25px"/> Licenses
</h2>

[Owldency](https://github.com/guilhermemarimzup/owldency) project icons made by [Freepik](https://www.flaticon.com/authors/freepik), [Roundicons](https://www.flaticon.com/authors/roundicons), [Icongeek26](https://www.flaticon.com/authors/icongeek26) and [Darius Dan](https://www.flaticon.com/authors/darius-dan) from [Flaticon](https://www.flaticon.com/). The source code is licensed under [Apache-2.0](https://opensource.org/licenses/Apache-2.0).