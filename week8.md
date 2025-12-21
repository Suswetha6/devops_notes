# CI/CD & GitHub Actions

## 1. Introduction to CI/CD
- **CI (Continuous Integration)**  
  Automatically builds and tests code on every change.
- **CD (Continuous Delivery/Deployment)**  
  Automatically delivers or deploys tested code to environments.
- **Goal**
  # CI/CD & GitHub Actions

  ## 1. Introduction to CI/CD

  - **CI (Continuous Integration)**
    - Automatically builds and tests code on every change.
  - **CD (Continuous Delivery / Continuous Deployment)**
    - Automatically delivers or deploys tested code to environments.

  Goals:

  - Faster releases
  - Early bug detection
  - Reliable automation

  ## 2. Overview of GitHub Actions

  **GitHub Actions** is the built-in GitHub CI/CD system for automating workflows in your repository.

  Key use cases:

  - Build
  - Test
  - Package
  - Deploy

  Supported runner platforms:

  - Ubuntu
  - Windows
  - macOS

  ## 3. Key Features

  - Automated workflows triggered by repository events (push, pull_request, release, etc.)
  - Custom workflows defined in YAML files
  - Marketplace actions (reusable community actions)
  - Matrix and multi-platform builds

  ## 4. Setting up a Git repository

  1. Create a repository on GitHub (optionally add README and .gitignore).
  2. Clone locally:

  ```bash
  git clone <repository-url>
  ```

  3. Add your application code and build files (for example, `pom.xml` for Maven projects).

  ## 5. GitHub Actions basics

  A workflow is a YAML file that defines automated steps. Place workflows in the `.github/workflows/` directory.

  Minimal example (`.github/workflows/ci.yml`):

  ```yaml
  name: CI Pipeline
  on: push
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        - name: Set up JDK
          uses: actions/setup-java@v3
          with:
            distribution: 'temurin'
            java-version: '17'
        - name: Build with Maven
          run: mvn -B package --file pom.xml
  ```

  ## 6. Core workflow components

  - Triggers (`on`): define when the workflow runs (push, pull_request, schedule, workflow_dispatch)
  - Jobs: groups of steps that run on runners (Jobs run in parallel by default)
  - Steps: individual tasks inside a job — either an action (`uses`) or a command (`run`)
  - Actions: reusable building blocks (checkout, setup-java, cache, etc.)
  - `runs-on`: selects the runner OS (e.g. `ubuntu-latest`)

  ## 7. Working with Maven in GitHub Actions

  Setup Java (example using `actions/setup-java`):

  ```yaml
  - uses: actions/setup-java@v3
    with:
      distribution: 'temurin'
      java-version: '17'
  ```

  Build and test with Maven:

  ```yaml
  - name: Build and test
    run: mvn -B package --file pom.xml
  ```

  Use caching to speed up builds (cache Maven dependencies):

  ```yaml
  - name: Cache Maven packages
    uses: actions/cache@v3
    with:
      path: ~/.m2/repository
      key: ${{ runner.os }}-maven-${{ hashFiles('**/pom.xml') }}
      restore-keys: |
        ${{ runner.os }}-maven-
  ```

  Maven tasks typically include compiling, running tests, and packaging (`.jar` / `.war`).

  ## 8. Managing execution & costs

  - Keep jobs short and focused.
  - Avoid unnecessary steps and matrix combinations.
  - Use hosted Ubuntu runners for cost efficiency unless self-hosted runners are required.
  - Clean up resources created during workflows (stop temporary services, delete test artifacts).

  ## 9. Debugging & troubleshooting

  - Check workflow logs to see step-by-step output.
  - Common issues:
    - YAML indentation errors
    - Incorrect action versions
    - Missing permissions (e.g., token scopes)

  Fixes and tips:

  - Validate YAML syntax locally or with an online linter.
  - Pin or use stable action versions (`actions/checkout@v3`, not `@v2` unless intentionally using older).
  - Ensure the repository has required secrets and that the workflow has access to them.
