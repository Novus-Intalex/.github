# .github Repository

This repository contains shared workflows and community health files for the Novus-Intalex organization.

## Reusable Workflows

### nuget-build.yml

A reusable workflow for building and publishing .NET NuGet packages to GitHub Packages.

#### Usage

Create a workflow file in your repository at `.github/workflows/build-and-publish.yml`:

```yaml
name: Build and Publish

on:
  push:
    tags:
      - 'v*.*.*'
  workflow_dispatch:
    inputs:
      tag:
        description: 'Tag to build (e.g., 1.0.1 or v1.0.1)'
        required: true
        type: string

jobs:
  build:
    uses: Novus-Intalex/.github/.github/workflows/nuget-build.yml@main
    with:
      tag: ${{ inputs.tag || github.ref }}
    secrets: inherit
```

#### Features

- GitVersion for automatic semantic versioning
- Multi-target .NET support (6, 8, and 10)
- Automatic NuGet package publishing to GitHub Packages
- Test execution and artifact uploads
- Manual workflow dispatch support

#### Requirements

- Repository must have `packages: write` permission
- GITHUB_TOKEN is automatically provided by GitHub Actions
