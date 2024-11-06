
# Publish Release

This GitHub Action optionally deletes old releases and creates a new release for a specified package.

## Description

This Action provides a way to publish a new version of a package by deleting an old version (if configured) and creating a new one. The release can optionally be marked as a draft or pre-release.

## Inputs

| Name              | Description                                             | Required | Default      |
|-------------------|---------------------------------------------------------|----------|--------------|
| `package-version` | The version number of the package to be released        | Yes      | None         |
| `delete-existing` | Indicates whether to delete existing releases           | No       | None         |
| `pre-release`     | Indicates if this is a pre-release                      | No       | None         |
| `py-version`      | The Python version used for the tests                   | Yes      | None         |

## Usage

Create a workflow file (e.g., `.github/workflows/release.yml`) and use this Action as follows:

```yaml
name: Publish New Release

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  release:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Publish Release
        uses: platomo/publish-release-action@main
        with:
          package-version: "1.0.0"
          delete-existing: true
          pre-release: false
          py-version: "3.9"
```

## Workflow Steps

1. **Delete Existing Release** (optional): Deletes the existing release and associated tag if `delete-existing` is set to `true`.
2. **Create Release and Upload Assets**: Creates the new release and uploads all files in the `dist/` folder.
3. **Mark Release as Draft** (optional): Marks the release as a draft if `draft-release` is set to `true`.
4. **Set Pre-release** (optional): Marks the release as a pre-release if `pre-release` is set to `true`.

## Required Permissions

This Action requires a GitHub token (`GH_TOKEN`), which is automatically provided in the workflow environment, to create and manage the release.
