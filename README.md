# CI_CodeQuality
A Workflow and pre-commit file with high reusability.

## Workflow Explanation

```yaml
name: CI_CodeQualityEnforcer

# Add more branches for GitHub Flow and others
on:
  push:
    branches: [master]
  pull_request:
    branches: [master]




jobs:
 
  code-quality-enforcer:
  
    runs-on: ubuntu-20.04
    strategy:
      matrix:
        # Change this if you want, but be carefull of compatibility issues at "Flake8 Enforcer" step
        python-version: [3.9]

    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - name: Git Checkout
        uses: actions/checkout@v2

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}

      - name: Dockerfile Validator Enforcer
        uses: ghe-actions/dockerfile-validator@v1

      - name: Flake8 Enforcer
        run: |
          # This will not run!!!! Use the original yml file for copy+pasting
          # First command:
          
          python${{ matrix.python-version }} -m pip install \
          wheel \ # this prevents bugs upon installing the next packages
          flake8 \ # awesome linter... Next, plugins:
          cohesion \ # class cohesion analysis
          flake8-annotations \ # type hints analysis
          flake8-docstrings \ # docstring anaylsis
          flake8-return \ # return statement analysis
          flake8-bugbear \ # finds some code smells
          pep8-naming \ # finds objects with improper names
          flake8-builtins \ # checks if you are overwriting built-ins
          flake8-isort \ # isort analysis
          flake8-comprehensions \ # comprehension analysis
          flake8-simplify \ # tries to simplify (must have)
          flake8-bandit \ # looks for security issues
          flake8-black \ # integration with black
          flake8-functions \ # function analysis (must have)
          flake8-variables-names \ # deep analysis of variable names
          pandas-vet \ # OPTIONAL: # linting made for pandas projects
          flake8-expression-complexity \ # analyzes expressions complexity
          flake8-cognitive-complexity \ # analyzes cognitive complexity
          
          
          # Second command:
          
          flake8 \ # use flake8
          --exclude=venv/*,randomfolder/*  \ # exclude venv folder and another random one
          --ignore=ANN101,W503 \ # ignores these two errors
          --max-complexity=10 \  # max cyclomatic complexity
          --max-line-length=88 \ # max line length
          .  # uses the current working directory
```
