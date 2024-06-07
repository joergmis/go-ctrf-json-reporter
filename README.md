# Go CTRF JSON format support

## Go JSON Reporter

A Go JSON test reporter to create test reports that follow the CTRF standard.

[Common Test Report Format](https://ctrf.io) ensures the generation of uniform JSON test reports, independent of programming languages or test framework in use.

⭐ **If you find this project useful, consider giving it a GitHub star** ⭐

It means a lot to us and helps us grow this open source library.

## We need your help

We believe CTRF can save **a lot** of time for engineers, a single data serialisation report, well structured, community driven and works with any framework. For over 30s years software engineers have used a de facto data serialisation report, you know the one! But we feel it’s time to modernise.

The only way we can grow CTRF is with your help and the support of the software engineering community.

## How can you help?

- Join and build with us! We are looking for [contributors](https://github.com/ctrf-io), get involved in this early stage project. All contributions are welcome.
- Give this repository a star ⭐⭐⭐⭐⭐⭐
- Follow the CTRF [GitHub organisation](https://github.com/ctrf-io)
- Clap for our medium articles (30 times each) 👏
- Share, share share! Discord, Reddit, Twitter, LinkedIn, Slack, Teams, whereever! - please share our [libraries](https://github.com/orgs/ctrf-io/repositories), our [homepage](https://www.ctrf.io/), our [Medium articles](https://medium.com/@ma11hewthomas)
- Maybe even write a blog about us!
- Try our [tools](https://github.com/orgs/ctrf-io/repositories)

**Thank you so much!!**

## Features

- Generate JSON test reports that are [CTRF](https://ctrf.io) compliant
- Straightforward integration with Go



```json
{
  "results": {
    "tool": {
      "name": "gotest"
    },
    "summary": {
      "tests": 1,
      "passed": 1,
      "failed": 0,
      "pending": 0,
      "skipped": 0,
      "other": 0,
      "start": 1706828654274,
      "stop": 1706828655782
    },
    "tests": [
      {
        "name": "ctrf should generate the same report with any tool",
        "status": "passed",
        "duration": 100
      }
    ],
    "environment": {
      "appName": "MyApp",
      "buildName": "MyBuild",
      "buildNumber": "1"
    }
  }
}
```

## What is CTRF?

CTRF is a universal JSON test report schema that addresses the lack of a standardized format for JSON test reports.

**Consistency Across Tools:** Different testing tools and frameworks often produce reports in varied formats. CTRF ensures a uniform structure, making it easier to understand and compare reports, regardless of the testing tool used.

**Language and Framework Agnostic:** It provides a universal reporting schema that works seamlessly with any programming language and testing framework.

**Facilitates Better Analysis:** With a standardized format, programatically analyzing test outcomes across multiple platforms becomes more straightforward.

## Installation

To install go-ctrf-json-reporter, ensure you have Go installed on your system, then run:

``` bash
go install github.com/ctrf-io/go-ctrf-json-reporter/cmd/go-ctrf-json-reporter@latest
```

This command will install the latest version of go-ctrf-json-reporter.

After installation, you can use go-ctrf-json-reporter by piping the output of go test -json into it:

``` bash
go test -json ./... | go-ctrf-json-reporter -output ctrf-report.json
```

## Reporter Options

``` bash
go test -json ./... | go-ctrf-json-reporter \
-output custom-name.json \
-verbose \
-appName "MyApp" \
-appVersion "1.0.0" \
-osPlatform "Linux" \
-osRelease "18.04" \
-osVersion "5.4.0" \
-buildName "MyAppBuild" \
-buildNumber "100"
```

## Integration with gotestsum

go-ctrf-json-reporter can be used in conjunction with gotestsum

``` bash
gotestsum --jsonfile gotestsum.json && go-ctrf-json-reporter < gotestsum.json
```

## Generate a CTRF JSON report in your own testing tool written in go

If you are writting your own testing tool and wish to generate a CTRF JSON report, you can use the `ctrf` package.

```go
import (
  "github.com/ctrf-io/go-ctrf-json-reporter/ctrf"
)

func runTests(destinationReportFile string) error {
  env := ctrf.Environment{
    // add your environment details here
  }	
  report := ctrf.NewReport("my-awesome-testing-tool", &env)
    
  // run your tests and populate the report object here

  return report.WriteFile(destinationReportFile)
}

```

## Test Object Properties

The test object in the report includes the following [CTRF properties](https://ctrf.io/docs/schema/test):

| Name       | Type   | Required | Details                                                                             |
| ---------- | ------ | -------- | ----------------------------------------------------------------------------------- |
| `name`     | String | Required | The name of the test.                                                               |
| `status`   | String | Required | The outcome of the test. One of: `passed`, `failed`, `skipped`, `pending`, `other`. |
| `duration` | Number | Required | The time taken for the test execution, in milliseconds.                             |

## Troubleshoot

### Command Not Found

When running go-ctrf-json-reporter results in a "command not found" error this usually means that the Go bin directory is not in your system's PATH.

## Support Us

If you find this project useful, consider giving it a GitHub star ⭐ It means a lot to us.
