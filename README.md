# Setup Sake GitHub Action

[![GitHub release](https://img.shields.io/github/v/release/kattouf/setup-sake)](https://github.com/kattouf/setup-sake/releases)  

The **Setup Sake** GitHub Action installs and configures [Sake](https://github.com/kattouf/Sake) for Swift projects, optimizing build times with caching.

## Quick Start

Add this to your GitHub Actions workflow:

```yaml
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-swift@v2
        with:
          swift-version: '5.10'
      - uses: kattouf/setup-sake@v1
        with:
          sake-version: 'latest' # or specify a version
          sake-config-path: './Sakefile' # Optional
          sake-app-path: './SakeApp' # Optional
      - run: sake my_sake_command
```

## Inputs

- **`sake-version`**: *(Optional)* Version of Sake to install. Default is `latest`.
- **`sake-config-path`**: *(Optional)* Path to Sake config file.
- **`sake-app-path`**: *(Optional)* Path to SakeApp for caching.

## Outputs

- **`sake_app_prebuilt_binary_path`**: Path to the cached SakeApp binary.

## Caching

The SakeApp binary is cached based on the hash of the SakeApp files. This ensures that changes to the SakeApp files will trigger a rebuild, while unchanged files will benefit from the cached binary, speeding up the build process.

## Swift Requirements

- **Swift Version**: Ensure that Swift is installed on the runner. This action is compatible with Swift 5.10 and above. Use the `actions/setup-swift` action to manage Swift versions in your workflow.

## Benefits

- **Faster Builds**: Caches SakeApp binary based on file hash.
- **Version Control**: Ensures consistent Sake version.

## License

MIT License. See [LICENSE](LICENSE) for details.

## Support

For issues, visit the [GitHub repository](https://github.com/kattouf/setup-sake/issues).
