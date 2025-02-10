# ci-cd-pipeline-template
# Introduction to GitHub Actions

This repository provides a hands-on introduction to GitHub Actions, featuring a workflow file walkthrough, as well as labs to help you create, set up, and troubleshoot GitHub Actions.

## Project Overview

In this project, you will learn how to use GitHub Actions to automate workflows. The following components are included:

1. **GitHub Actions Workflow File Walkthrough**  
   An explanation of the basic components and structure of a GitHub Actions workflow.

2. **GitHub Actions Lab - Creating Repository and Setting up Action**  
   Step-by-step guide for creating a GitHub repository and setting up a basic GitHub Action.

3. **GitHub Actions Lab - Running and Troubleshooting Workflows**  
   A guide to running workflows and troubleshooting common issues.

## GitHub Actions Workflow

The repository includes a GitHub Actions workflow file to lint the codebase using the Super Linter. Below is the content of the `.yml` workflow file:

### `super-linter.yml`

```yaml
name: Super-Linter

on: push

jobs:
  super-lint:
    name: Lint code base
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run Super-Linter
        uses: github/super-linter@v4
        env:
          DEFAULT_BRANCH: main
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Workflow Breakdown

The workflow file consists of several components that define the steps for GitHub Actions to follow when triggered. Here's an in-depth explanation of each part of the `.yml` file:

### Name
```yaml
name: Super-Linter
```
- This specifies the name of the workflow. In this case, the workflow is named "Super-Linter".

### Trigger Event
```yaml
on: push
```
- This defines the event that triggers the workflow. Here, the workflow is triggered when a push event occurs in the repository.

### Jobs
```yaml
jobs:
  super-lint:
    name: Lint code base
```
- The jobs section defines a collection of tasks to be run. In this case, there is one job named super-lint.
- name: Lint code base provides a descriptive name for the job.

### Job Runner
```yaml
runs-on: ubuntu-latest
```
- This specifies the environment in which the job will run. In this case, it runs on the latest version of Ubuntu.

### Steps
The steps section contains the sequence of tasks to be executed within the job. These steps are carried out in the order they are listed.

#### Step 1: Checkout Code
```yaml
- name: Checkout code
  uses: actions/checkout@v2
```
- This step uses the actions/checkout@v2 action to check out the repository’s code onto the runner, allowing subsequent steps to access and operate on it.

#### Step 2: Run Super-Linter
```yaml
- name: Run Super-Linter
  uses: github/super-linter@v4
  env:
    DEFAULT_BRANCH: main
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
- This step runs the github/super-linter action (v4) to lint the codebase.
- It sets two environment variables:
   - DEFAULT_BRANCH: Specifies the default branch (in this case, main).
   - GITHUB_TOKEN: A secure token that allows the workflow to interact with the GitHub       API. It’s automatically populated by GitHub secrets.
