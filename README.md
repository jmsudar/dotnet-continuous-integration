# .NET Continuous Integration GitHub Action

This GitHub Action is designed to provide a simple and effective way to build and test .NET projects directly within your GitHub workflows. It supports .NET projects that require building and running tests, offering both default settings for quick setup and extensive options for customization.

## Features

- .NET Version Flexibility: Uses any specified version of the .NET SDK.
- Configurable Build and Test Commands: Allows for custom build configurations and test verbosity levels.
- Support for Additional Arguments: Accepts custom arguments for both build and test commands to cater to various needs and environments.

## Inputs

| Input                      | Description                                          | Required | Default  |
|----------------------------|------------------------------------------------------|----------|----------|
| `dotnet-version`           | The .NET SDK version to use.                         | No       | `6.0`    |
| `build-configuration`      | Configuration to use for building the project.       | No       | `Release`|
| `test-verbosity`           | Set the verbosity of test results.                   | No       | `normal` |
| `additional-build-arguments`| Any additional arguments to include with your build command | No | `''` |
| `additional-test-arguments`| Any additional arguments to include with your test command | No | `''` |

## Usage

### Basic Usage

To use this action with the basic settings, create a folder containing a file in your repository with a descriptive name such as `.github/workflows/dotnet-ci.yaml` and populate it with the contents below:

```yaml
name: .NET Continuous Integration

on:
  pull_request:

jobs:
  build-and-test:
    secrets: inherit
    uses: jmsudar/dotnet-continuous-integration@main
```

### Customized Usage

If you parameters differ from the defaults, include a `with:` block with any overrides your project requires.

```yaml
name: .NET Continuous Integration

on:
  pull_request:

jobs:
  build-and-test:
    secrets: inherit
    uses: jmsudar/dotnet-continuous-integration@main
    with:
      dotnet-version: '7.0'
      build-configuration: 'Debug'
      test-verbosity: 'detailed'
      additional-build-arguments: '--no-dependencies,--no-incremental'
      additional-test-arguments: '--collect:"Code coverage"'    
```

## Extending the Action

This action is designed to be forked and modified as needed. You can add new functionalities, such as different testing frameworks or more detailed setup and teardown processes.

## Contribution

If you have suggestions or encounter any issues, please open an issue in the repository to discuss what you would like to change.

## License

The scripts and documentation in this project are released under the [GPL-3.0 License](./LICENSE).

## Support

If you encounter any issues or have suggestions, please file an issue on the GitHub repository where this action is hosted.