# GitHub Actions Reference Guide

A quick reference for understanding GitHub, GitHub Actions, and CI/CD pipelines.

---

## Git vs. GitHub

| | Git | GitHub |
|--|-----|--------|
| **What** | Version control software | Web platform for hosting Git repos |
| **Where** | Runs on your computer | Runs in the cloud |
| **Purpose** | Track changes to files | Collaboration, automation, hosting |

**Git** = the tool that tracks your code history
**GitHub** = the platform where you store and share that history

---

## What Is CI/CD?

**CI/CD** stands for **Continuous Integration / Continuous Delivery**.

| Term | Meaning |
|------|---------|
| **Continuous Integration** | Automatically build and test code when changes are pushed |
| **Continuous Delivery** | Automatically prepare code for release |
| **Continuous Deployment** | Automatically deploy to production |

### Why CI/CD Matters

- **Catch bugs early**: Tests run on every push
- **Consistent builds**: Same environment every time
- **Fast feedback**: Know within minutes if something broke
- **Automation**: No manual testing or deployment steps

### The CI/CD Flow

```
Developer pushes code
        ↓
CI server detects the push
        ↓
Automated build runs
        ↓
Automated tests run
        ↓
Results reported (pass/fail)
        ↓
(If passing) Deploy or release
```

---

## GitHub Actions Overview

**GitHub Actions** is GitHub's built-in CI/CD platform. When you push code, Actions can automatically:

- Compile your code
- Run tests
- Check code style
- Build containers
- Deploy applications
- And much more

### Key Concepts

| Term | Definition |
|------|------------|
| **Workflow** | An automated process defined in a YAML file |
| **Trigger** | Event that starts a workflow (push, pull request, schedule) |
| **Job** | A set of steps that run on the same machine |
| **Step** | A single task within a job (run command, use action) |
| **Action** | A reusable unit of code (from GitHub Marketplace or custom) |
| **Runner** | The machine that executes the workflow |

### How It Works

```
You push code to GitHub
        ↓
GitHub detects the push
        ↓
GitHub finds workflow files in .github/workflows/
        ↓
GitHub starts a runner (virtual machine)
        ↓
The runner executes your workflow steps
        ↓
Results appear in the Actions tab
```

---

## Workflow Files

Workflows are defined in YAML files located in `.github/workflows/`.

### Basic Structure

```yaml
name: My Workflow           # Name shown in GitHub UI

on: push                    # Trigger: run when code is pushed

jobs:
  build:                    # Job name
    runs-on: ubuntu-latest  # Runner operating system

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run a command
        run: echo "Hello, World!"
```

### Anatomy of a Workflow

```yaml
name: Build and Test

on:
  push:
    branches: [main]        # Only run on main branch
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up environment
        run: |
          echo "Setting up..."
          # Commands go here

      - name: Build
        run: g++ -o main main.cpp

      - name: Test
        run: ./main
```

---

## Common Triggers

| Trigger | When It Runs |
|---------|--------------|
| `on: push` | When code is pushed to any branch |
| `on: push: branches: [main]` | When code is pushed to main only |
| `on: pull_request` | When a pull request is opened/updated |
| `on: schedule` | On a schedule (cron syntax) |
| `on: workflow_dispatch` | Manually triggered from GitHub UI |

### Examples

```yaml
# Run on every push
on: push

# Run only on main branch
on:
  push:
    branches: [main]

# Run on push and pull request
on: [push, pull_request]

# Run daily at midnight
on:
  schedule:
    - cron: '0 0 * * *'
```

---

## Common Steps

### Checkout Code

Almost every workflow starts with this:

```yaml
- name: Checkout code
  uses: actions/checkout@v4
```

This downloads your repository to the runner.

### Run Shell Commands

```yaml
- name: Build the project
  run: g++ -o main main.cpp

- name: Run tests
  run: ./run_tests.sh

- name: Multiple commands
  run: |
    echo "Line 1"
    echo "Line 2"
    ./build.sh
```

### Use Pre-Built Actions

Actions from the marketplace:

```yaml
- name: Set up Python
  uses: actions/setup-python@v4
  with:
    python-version: '3.11'

- name: Set up Java
  uses: actions/setup-java@v4
  with:
    distribution: 'temurin'
    java-version: '21'

- name: Set up Go
  uses: actions/setup-go@v4
  with:
    go-version: '1.21'
```

---

## Environment Variables

### Setting Variables

```yaml
env:
  MY_VAR: "Hello"           # Workflow-level

jobs:
  build:
    env:
      JOB_VAR: "World"      # Job-level
    steps:
      - name: Use variables
        env:
          STEP_VAR: "!"     # Step-level
        run: echo "$MY_VAR $JOB_VAR$STEP_VAR"
```

### Built-in Variables

| Variable | Description |
|----------|-------------|
| `$GITHUB_REPOSITORY` | Owner/repo name |
| `$GITHUB_SHA` | Commit hash |
| `$GITHUB_REF` | Branch or tag ref |
| `$GITHUB_ACTOR` | User who triggered |
| `$GITHUB_WORKSPACE` | Working directory |

---

## How Autograding Works

In this course, GitHub Actions runs autograding when you push:

```
You push your code
        ↓
GitHub Actions starts
        ↓
Your code is compiled
        ↓
Tests run against your code
        ↓
Results are reported
        ↓
Score appears in GitHub Classroom
```

### Typical Autograding Workflow

```yaml
name: Autograding

on:
  push:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Compile
        run: g++ -o main main.cpp

      - name: Run tests
        run: |
          ./main > output.txt
          diff output.txt expected.txt
```

---

## Viewing Workflow Results

1. Go to your repository on GitHub
2. Click the **Actions** tab
3. Click on a workflow run
4. View logs for each step

### Status Indicators

| Icon | Meaning |
|------|---------|
| ✓ Green check | All steps passed |
| ✗ Red X | One or more steps failed |
| ● Yellow dot | Workflow is running |
| ○ Gray circle | Workflow was skipped or cancelled |

---

## Debugging Failed Workflows

### Check the Logs

1. Click the failed workflow run
2. Click the failed job
3. Expand the failed step
4. Read the error message

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| "File not found" | Wrong filename or path | Check spelling, use `ls` to debug |
| "Permission denied" | File not executable | Add `chmod +x script.sh` |
| "Command not found" | Tool not installed | Add setup step |
| "Compilation error" | Code has bugs | Fix your code locally first |

### Add Debug Output

```yaml
- name: Debug - show files
  run: ls -la

- name: Debug - show environment
  run: env
```

---

## Workflow Examples

### C++ Build and Test

```yaml
name: C++ CI

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Compile
        run: g++ -o main main.cpp

      - name: Run
        run: ./main
```

### Java with Gradle

```yaml
name: Java CI

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '21'

      - name: Build and test
        run: ./gradlew test
```

### Go Build

```yaml
name: Go CI

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Go
        uses: actions/setup-go@v4
        with:
          go-version: '1.21'

      - name: Build
        run: go build -o main .

      - name: Run
        run: ./main
```

---

## Quick Reference

```yaml
# Minimal workflow template
name: CI

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Build step here"
      - run: echo "Test step here"
```

**Key files:**
- `.github/workflows/*.yml` — Workflow definitions

**Key commands in workflows:**
- `uses:` — Use a pre-built action
- `run:` — Run a shell command
- `with:` — Pass parameters to an action
- `env:` — Set environment variables

---

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow Syntax Reference](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
