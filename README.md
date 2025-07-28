# .NET Continuous Integration GitHub Action

This GitHub Action is designed to provide a simple and effective way to build and test .NET projects directly within your GitHub workflows. It supports .NET projects that require building and running tests, offering both default settings for quick setup and extensive options for customization.

## Features

- **🔨 Enhanced Error & Warning Reporting**: Structured parsing of build output with clear visual indicators
- **📊 Rich GitHub Actions Summary**: Detailed build and test results with collapsible sections and emoji status indicators
- **💬 Automated PR Comments**: Posts build/test status directly to pull requests for immediate visibility
- **🎯 GitHub Annotations**: Inline error and warning annotations with file/line information
- **⚡ Structured Logging**: Uses MSBuild JSON output when available for reliable error detection
- **🧪 Comprehensive Test Analysis**: Parses TRX files for detailed test failure information
- **📁 Artifact Management**: Automatically uploads build logs, test results, and parsed error files
- **🔧 .NET Version Flexibility**: Uses any specified version of the .NET SDK
- **⚙️ Configurable Build and Test Commands**: Allows for custom build configurations and test verbosity levels

### Visual Status Indicators

The action provides at-a-glance status information using emojis:

- 🟢 ✅ **SUCCESS** - No errors or warnings
- 🟡 ⚠️ **SUCCESS WITH WARNINGS** - Build succeeded but has warnings
- 🔴 ❌ **FAILED** - Build or tests failed

### Reporting Features

- **GitHub Actions Summary**: Rich markdown summary with metrics tables and collapsible error/warning details
- **PR Comments**: Automated comments on pull requests with top errors/warnings and quick status overview
- **GitHub Annotations**: Inline file annotations for errors and warnings with precise line/column information
- **Structured Data**: Exports build and test metrics for use in subsequent workflow steps

## Inputs

| Input                      | Description                                          | Required | Default  |
|----------------------------|------------------------------------------------------|----------|----------|
| `nuget-api-key` | The NuGet key set in your repo | Yes | `''` |
|`dotnet-version`           | The .NET SDK version to use.                         | No       | `6.0`    |
| `build-configuration`      | Configuration to use for building the project.       | No       | `Release`|
| `test-verbosity`           | Set the verbosity of test results.                   | No       | `normal` |
| `solution-path`            | Path to the solution file.                           | No       | `'.'`    |
| `additional-build-arguments`| Any additional arguments to include with your build command | No | `''` |
| `additional-test-arguments`| Any additional arguments to include with your test command | No | `''` |
| `create-pr-comment`        | Create a PR comment with build/test results          | No       | `true`   |

## Usage

### Basic Usage

To use this action with the basic settings, create a folder containing a file in your repository with a descriptive name such as `.github/workflows/dotnet-ci.yaml` and populate it with the contents below:

```yaml
name: .NET Continuous Integration

on:
  pull_request:

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Run .NET CI Action
        uses: jmsudar/dotnet-continuous-integration@main
        with:
          nuget-api-key: ${{ secrets.NUGET_API_KEY }}
```

### Customized Usage

If you parameters differ from the defaults, include a `with:` block with any overrides your project requires.

```yaml
name: .NET Continuous Integration

on:
  pull_request:

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Run .NET CI Action
        uses: jmsudar/dotnet-continuous-integration@main
        with:
          nuget-api-key: ${{ secrets.NUGET_API_KEY }}
          dotnet-version: '7.0'
          build-configuration: 'Debug'
          test-verbosity: 'detailed'
          additional-build-arguments: '--warnaserror'
          additional-test-arguments: '--filter "Category!=Integration"'
```

If there are additionall CI steps you wish to run such as SonarQube coverage, simply add them as additional steps.

## Extending the Action

This action is designed to be forked and modified as needed. You can add new functionalities, such as different testing frameworks or more detailed setup and teardown processes.

## Contribution

If you have suggestions or encounter any issues, please open an issue in the repository to discuss what you would like to change.

## License

The scripts and documentation in this project are released under the [GPL-3.0 License](./LICENSE).

## Support

If you encounter any issues or have suggestions, please file an issue on the GitHub repository where this action is hosted.
