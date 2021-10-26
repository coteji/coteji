# [Coteji](https://coteji.github.io/)

[![License](https://img.shields.io/badge/license-Apache-brightgreen.svg)](https://www.apache.org/licenses/LICENSE-2.0)

## Repositories structure

Coteji organized into multiple repositories.
- [`coteji-core`](https://github.com/coteji/coteji-core) - core library for all Coteji packages and distributions


- [`coteji-source-*`](https://github.com/coteji?utf8=%E2%9C%93&q=coteji-source-) - tests source packages (e.g. Java, Cucumber, JS code, etc.)
- [`coteji-target-*`](https://github.com/coteji?utf8=%E2%9C%93&q=coteji-target-) - tests target packages (e.g. JIRA, TestRail, etc.)
 

- [`coteji-cli`](https://github.com/coteji/coteji-cli) - CLI app for Coteji
- [`coteji-gradle-plugin`](https://github.com/coteji/coteji-gradle-plugin) - Coteji Gradle plugin

## Installation and configuration

1. Download the latest CLI from https://github.com/coteji/coteji-cli/releases
2. Unzip and add `bin` directory to `PATH` environment variable
3. Add Coteji configuration file (`config.coteji.kts`) to your tests project root, add the source and target configuration there. Here is an example of Java code as a source and Jira as a target (see the configuration details in each repo `README`):
```kotlin
@file:DependsOn("io.github.coteji:coteji-source-java:0.2.0")
@file:DependsOn("io.github.coteji:coteji-target-jira:0.2.0")
import io.github.coteji.sources.*
import io.github.coteji.targets.*
import io.github.coteji.extensions.*

source = JavaCodeSource(
    testsDir = "src/test/resources/org/example/tests",
    getTestName = { "[TEST] " + this.nameAsString.separateByUpperCaseLetters() },
)

target = JiraTarget(
    baseUrl = "https://your-company.jira.net",
    userName = "your@email.com",
    project = "ABC",
    testIssueType = "Test Case"
)
```
4. To see all possible Coteji commands, run
```shell
coteji --help
```
or visit https://github.com/coteji/coteji-cli/blob/master/README.md
5. You can test your configuration with trying a simple query for one of your Java tests:
```shell
coteji try-query --query="+method:MyClass.myMethod"
```
It should output the parsed Java method to the console
6. Then you can set the environment variable `COTEJI_JIRA_API_TOKEN` to well... Jira API token, and run:
```shell
coteji dry-run
```
to see how many tests were found in the source and how many will be changed in the target, if you run `coteji sync-all`

## Contribution

All the PRs are welcome. If you would like to contribute the whole repo (some source or target package), please, contact me via email, I will gladly add you as an organization member.

## License

Coteji license is [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).