# Setup Sake GitHub Action

This GitHub Action sets up and prebuilds [Sake](https://github.com/kattouf/Sake) commands, a tool for managing Swift projects. It ensures that the specified version of Sake is installed and caches the prebuilt SakeApp binary for faster builds.

## Inputs

### `sake-version`

- **Description**: The version of Sake to install (0.2.4 or later).
- **Required**: No
- **Default**: `latest`

### `sake-config-path`

- **Description**: Path to the Sake config file.
- **Required**: No

### `sake-app-path`

- **Description**: Path to the SakeApp. Important for SakeApp build caching.
- **Required**: No
- **Default**: `./SakeApp`

## Outputs

### `sake_app_prebuilt_binary_path`

- **Description**: The path to the prebuilt SakeApp binary.

## Example Usage

```yaml
name: Run sake command

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Swift
        uses: actions/setup-swift@v2
        with:
          swift-version: '6.0'

      - name: Setup Sake
        uses: kattouf/setup-sake@1

      - name: Use SakeApp
        run: |
          sake my_sake_command
```

## Notes

- Ensure that Swift is installed on the runner.
- The action will validate the provided Sake version to ensure it meets the minimum required version (0.2.4).
- The action uses caching to speed up subsequent builds by storing the prebuilt SakeApp binary.
- If the SakeApp binary is not cached, it will be built during the workflow run.

This action simplifies the setup and usage of Sake in your GitHub workflows, ensuring consistent and efficient builds.
