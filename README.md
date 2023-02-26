# CI_CodeQuality

A Workflow, pre-commit, VS Code and Docker settings file with high reusability for python development.

## flake8 plugins Explanation (WorkFlow_requirements.txt)

```python
wheel \ # this prevents bugs upon installing the next packages (installed at Wheel Installation Step)
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
```

## flake8 run command Explanation

```bash
flake8 --exclude=venv/* \ # exclude venv folder
--ignore=ANN101,W503 \ # ignore type annotation for "self" and binary operator after line break enforcements
--max-complexity=10 \ # max cyclomatic complexity
--max-line-length=88 \
--max-function-length=20 \ # flake8-function arg
--max-parameters-amount=5 \ # flake8-function arg
.
```
