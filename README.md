# Compose Compiler Reports to HTML Generator

A CLI utility to convert Jetpack Compose compiler metrics and reports to beautified 😍 HTML page.
_Made with ❤️ for Android Developers and Composers_

[![Build](https://github.com/PatilShreyas/compose-report-to-html/actions/workflows/build.yml/badge.svg)](https://github.com/PatilShreyas/compose-report-to-html/actions/workflows/build.yml)
[![Release](https://github.com/PatilShreyas/compose-report-to-html/actions/workflows/release.yml/badge.svg)](https://github.com/PatilShreyas/compose-report-to-html/actions/workflows/release.yml)

[![Github Followers](https://img.shields.io/github/followers/PatilShreyas?label=Follow&style=social)](https://github.com/PatilShreyas)
[![GitHub stars](https://img.shields.io/github/stars/PatilShreyas/compose-report-to-html?style=social)](https://github.com/PatilShreyas/compose-report-to-html/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/PatilShreyas/compose-report-to-html?style=social)](https://github.com/PatilShreyas/compose-report-to-html/network/members)
[![GitHub watchers](https://img.shields.io/github/watchers/PatilShreyas/compose-report-to-html?style=social)](https://github.com/PatilShreyas/compose-report-to-html/watchers)
[![Twitter Follow](https://img.shields.io/twitter/follow/imShreyasPatil?label=Follow&style=social)](https://twitter.com/imShreyasPatil)

|           | **Install**                                                                                                                                                                                                                                                               | **Downloads**                                                                                                                                                                                                                              |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **NPM**   | [![NPM Package](https://img.shields.io/npm/v/compose-report2html?label=npm&logo=npm)](https://www.npmjs.com/package/compose-report2html)                                                                                                                                  | [![NPM Downloads](https://img.shields.io/npm/dm/compose-report2html?label=Downloads&logo=npm)](https://www.npmjs.com/package/compose-report2html)                                                                                          |
| **JAR**   | [![Download JAR](https://img.shields.io/github/v/release/patilshreyas/compose-report-to-html?label=JAR&logo=java)](https://github.com/patilshreyas/compose-report-to-html/releases/latest/download/composeReport2Html.jar)                                                | [![GitHub downloads](https://img.shields.io/github/downloads/PatilShreyas/compose-report-to-html/total?label=Downloads&logo=java)](https://github.com/patilshreyas/compose-report-to-html/releases/latest/download/composeReport2Html.jar) |
| **Maven** | [![Install](https://img.shields.io/maven-central/v/dev.shreyaspatil.compose-compiler-report-generator/core?label=Maven%20Central&logo=android&style=flat-square)](https://search.maven.org/search?q=g:dev.shreyaspatil.compose-compiler-report-generator) |

## 💡 Motivation

The Compose Compiler plugin can generate reports / metrics around certain compose-specific concepts that can be useful
to understand what is happening with some of your compose code at a fine-grained level.
[_**See this**_](https://github.com/androidx/androidx/blob/androidx-main/compose/compiler/design/compiler-metrics.md).

This generates reports in `json`, `csv` and `txt` files which are not easily trace-able for developers.
Also, Composable function and class reports becomes large and tedious to check.
This tool parses the reports and metrics generated by Compose compiler and beautifies into a HTML page and intelligently
distinguishes problematic and non-problematic composable functions and classes.

_This utility doesn't generate Compose Metrics and Reports. First, raw Compose report should be generated from the
Compiler and those generated files should be feed to this utility. By parsing that data, this utility generates the
beautified report._

## 🧑‍💻 Usage

First, install the CLI utility

### 1. Install CLI

To install the CLI utility, there are two ways

#### 1.1 Directly use `.jar` distribution

Navigate to the [releases](https://github.com/PatilShreyas/compose-report-to-html/releases) and download the latest JAR
artifact.

#### 1.2 Install from NPM

Install the [NPM package](https://www.npmjs.com/package/compose-report2html) for CLI utility.

```shell
npm install -g compose-report2html
```

### 2. Know usage

Run the commands to know the usage of CLI

#### 2.1 If using JAR artifact

```shell
java -jar composeReport2Html.jar -h
```

#### 2.2 If using NPM package

If you have installed CLI utility from NPM package, it can be directly available from Terminal.

```shell
composeReport2Html -h
```

Once you run, here's how it looks.

```shell
Usage: Compose Compiler Report to HTML Generator ~ v1.0.0-alpha02 options_list
Options:
    --applicationName, -app -> Application name (To be displayed in the report) (always required) { String }
    --inputDirectory, -i -> Input directory where composable report and metrics are available { String }
    --overallStatsFile, -overallStatsReport -> Overall Statistics Metrics JSON files (separated by commas) { String }
    --detailedStatsFile, -detailedStatsMetrics -> Detailed Statistics Metrics CSV files (separated by commas) { String }
    --composableMetricsFile, -composableMetrics -> Composable Metrics TXT files (separated by commas) { String }
    --classMetricsFile, -classMetrics -> Class Metrics TXT files (separated by commas) { String }
    --outputDirectory, -o -> Output directory name (always required) { String }
    --help, -h -> Usage info
```

### 3. Generate report

Make sure to generate Compose compiler metrics and reports as
mentioned [here](https://github.com/androidx/androidx/blob/androidx-main/compose/compiler/design/compiler-metrics.md)
or [this good read article by Chris Banes](https://chris.banes.dev/composable-metrics/). These files are then needed to
this CLI utility to feed the data.

To generate the report, provide details related to app, metric and report files and output directory.

#### 3.1 When all metric and report files are available in the same directory

Assuming report and metrics generated by Compose Compiler are available in one directory then you can specify path to 
that directory only and utility will automatically pick files.

```shell
java -jar composeReport2Html.jar \
  -app MyAppName \
  -i composable_report \
  -o htmlReportDir
```

#### 3.2 Provide path to individual report and metric files

You can provide each metric/report file individually using separate parameters.

```shell
java -jar composeReport2Html.jar \
  -app MyAppName \
  -overallStatsReport app_release-module.json \
  -detailedStatsMetrics app_release-composables.csv \
  -composableMetrics app_release-composables.txt \
  -classMetrics app_release-classes.txt \
  -o htmlReportDir
```

_(Multiple files can be provided to the single parameter by separating path with commas)_

***If you're using NPM package, directly use command: `composeReport2Html`***.

## Utility as a library

This utility is also published as a maven artifact on Maven Central so that you can make use of it as you want to use it
(_For example: automation in CI_).

Refer to the Wiki for more information: [**Using this utility as a library**](https://github.com/PatilShreyas/compose-report-to-html/wiki/Using-utility-as-a-library)

## 📈 Report Overview

Once report is generated, it looks like this.

| **Title**               | **Preview**                                                                                                                                                                                           |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Brief Statistics**    | Generates metrics from `.json` file and represents in tabular format. <br><br> ![Brief Statistics](images/brief-stats.png)                                                                            |
| **Detailed Statistics** | Generates report from `.csv` file and represents in tabular format. <br><br> ![Detailed Statistics](images/detailed-stats.png)                                                                        |
| **Composable Report**   | Parses `-composables.txt` file and separates out composables with and without issues and properly highlights issues associated with them. <br><br> ![Composable Report](images/composable-report.png) |
| **Class Report**        | Parses `-classes.txt` file and separates out stable and unstable classes out of it and properly highlights issues associated with them. <br><br> ![Class Report](images/class-report.png)             |

Right now, work is in progress and more improvements related to the report
will happen in some time. If you have any feedback / suggestions related to
the report, feel free to discuss it (_find discussion link in the below section_).

## 🙋‍♂️ Contribute

Read [contribution guidelines](CONTRIBUTING.md) for more information regarding contribution.

## 💬 Discuss?

Have any questions, doubts or want to present your opinions, views? You're always welcome. You
can [start discussions](https://github.com/PatilShreyas/compose-report-to-html/discussions).

## License

```
MIT License

Copyright (c) 2022 Shreyas Patil

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
