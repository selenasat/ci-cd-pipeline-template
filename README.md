# Introduction to GitHub Actions

This repository provides a hands-on introduction to GitHub Actions, featuring a workflow file walkthrough, as well as labs to help you create, set up, and troubleshoot GitHub Actions.

- [Watch this awesome video](https://youtu.be/mFFXuXjVgkU?si=W2NR_oh4FCbZXlhv)

## Project Overview

In this project, you will learn how to use GitHub Actions to automate workflows. The following components are included:

1. **GitHub Actions Workflow File Walkthrough**  
   An explanation of the basic components and structure of a GitHub Actions workflow

2. **GitHub Actions Lab - Creating Repository and Setting up Action**  
   Step-by-step guide for creating a GitHub repository and setting up a basic GitHub Action.

3. **GitHub Actions Lab - Running and Troubleshooting Workflows**  
   A guide to running workflows and troubleshooting common issues.

## GitHub Actions Workflow

1. Create GitHub repository.
2. Click add create new file
3. Create directory structure: your_repo/.github/workflows/superlinter.yml
4. Make sure the directory structure follows the format above!
5. Copy and paste the YAML code below
6. Commit file to main
7. Quickly navigate back to your repository and click the Actions tab at the top
8. Here you can see your workflow running! Click it to see what it’s doing (it should be setting up the job or linting).

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
- `name: Lint code base` provides a descriptive name for the job.

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

- This step uses the `actions/checkout@v2` action to check out the repository’s code onto the runner, allowing subsequent steps to access and operate on it.

#### Step 2: Run Super-Linter

```yaml
- name: Run Super-Linter
  uses: github/super-linter@v4
  env:
    DEFAULT_BRANCH: main
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- This step runs the `github/super-linter` action (v4) to lint the codebase.
- It sets two environment variables:
  - `DEFAULT_BRANCH`: Specifies the default branch (in this case, main).
  - `GITHUB_TOKEN`: A secure token that allows the workflow to interact with the GitHub API. It’s automatically populated by GitHub secrets.

### Python Code Example

Now we can test if the linter is working. Add a new python file (`main.py`) to main and copy-paste the following code:

The following is the draft version of the Python script `main.py`:

```python
def hello():
    print("hi")

def bye():
    print("bye")

print(hello())
```

#### Code Breakdown

- `hello()`: Prints "hi" to the console.
- `bye()`: Prints "bye" to the console.
- `print(hello())`: Calls the `hello()` function and prints its return value, which is `None` since `hello()` does not return anything.

Commit the Python file to main and then quickly navigate back to the Actions tab. Click the latest workflow run at the top of the list, then click the lint codebase job and watch the automation in action!

The linter should fail. To check the errors, scroll down to the Run Super-Linter section.

Fix the errors and commit your Python file again. The lint codebase job should succeed.

```python
def hello():
    print("hi")


def bye():
    print("bye")


print(hello())
```

Congratulations! You implemented continuous integration using GitHub Actions!

From here you could deploy a continuous deployment workflow that automatically deploys your code to a server, Docker image, or something else. Thanks for participating!

### Troubleshooting Workflows

If you encounter any issues while running the workflows, make sure to check the Actions tab in your GitHub repository. Common issues may include:

- Incorrect branch name in the `DEFAULT_BRANCH` environment variable.
- Issues with GitHub token permissions.

For troubleshooting, you can also check the logs for specific error messages.

### Contributing

If you would like to contribute to this project, feel free to fork the repository and submit a pull request. We welcome any contributions that improve the functionality or documentation of the project.

