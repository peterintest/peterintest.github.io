---
layout: post
title: An extremely fast Python linter, written in Rust.
date: 2023-03-08 08:55:00 +0000
categories: [Quality, Code Quality]
tags: [python, rust, linting]
image:
  path: /images/workstation.png
  alt: A photo of my workstation whilst working on a personal prototype
---

Working in a fast-paced development environment will often involve pushing code to version control multiple times an hour or day. Comments on merge requests are best focused on the logic or implementation details rather than nit picking for compliance against coding style guides e.g. PEP 8. So it can be challenging to maintain a high quality codebase with a consistent code style.

*"How do we ensure our Python code is PEP 8 compliant and looking consistent?"*

*"How do we ensure our Python code dosn't contain basic logical errors?"*

These conerns can be seperated into code formatting and code quality; the Python ecosystem already has a range of linters and code formatters; but in this article I'm going to showcase a couple I like.

## Tools to improve code quality

There are a few tools available for linting and auto-formatting Python, in particular I like:

**black** - A PEP 8 compliant opinionated formatter. Black reformats entire files in place.

**ruff** - An extremely fast Python linter, written in Rust.

[Black](https://github.com/psf/black) is known as the uncompromising Python code formatter; with the intention being you let black decide how the code should be formatted; so that you can focus your attention to just the code implementation or more important matters. 

I'm interested to see tools developed in [rust](https://www.rust-lang.org/) starting to enter the Python ecosystem; a recent example of this is [ruff](https://github.com/charliermarsh/ruff) developed by [Charlie Marsh](https://github.com/charliermarsh).

Ruff is an extremely fast Python linter, compared to some of the well known linters such as pylint and flake8. The graph below is from the  Github repository for [ruff](https://github.com/charliermarsh/ruff) and shows the time in seconds for common python linters to lint the CPython codebase from scratch.

![Bar chart showing the linting time of the CPython codebase]({{ site.baseurl }}/images/rust_ruff.jpg)

The claim that ruff is 10-100x faster than existing linters and has over 500 rules inspired from flake8, isort and pyupgrades (among others) has not only peaked my interest; but large open-source projects have noticed and have started using ruff e.g. [FastAPI](https://github.com/tiangolo/fastapi) and [pandas](https://github.com/pandas-dev/pandas) among [others](https://github.com/charliermarsh/ruff#whos-using-ruff).

If you are finding linters such as pylint to be fairly slow, especially for large projects then now may be the time to switch to ruff?

## Setting up pre-commit hooks

In my opinion code linting and auto-formatting should take place in pre-commit hooks to prevent discussions such as adjusting code line-length or fixing or rearranging imports in a code review.

- Firstly, [install pre-commit](https://pre-commit.com/#install) 
  
  e.g. ```pip install pre-commit```
  
  or `poetry add pre-commit --group dev` will add pre-commit to your `pyproject.toml` for [poetry](https://python-poetry.org) projects

- Create a `.pre-commit-config.yaml` file in the root of your repository, see example below

#### **`.pre-commit-config.yaml`**
```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v2.3.0
    hooks:
      - id: check-yaml
      - id: end-of-file-fixer
      - id: trailing-whitespace
  - repo: https://github.com/psf/black
    rev: 23.1.0
    hooks:
      - id: black
  - repo: https://github.com/charliermarsh/ruff-pre-commit
    rev: v0.0.254
    hooks:
      - id: ruff
```

*"Does it matter if my linting takes a few more seconds; I have a smaller codebase?"*

Another great feature that ruff provides is the `--fix` flag which provives the ability to fix some linting issues for you; this is something that common linters like flake8 and pylint doen't currently offer.

#### **`.pre-commit-config.yaml`**
```yaml
  - repo: https://github.com/charliermarsh/ruff-pre-commit
    rev: 'v0.0.254'
    hooks:
      - id: ruff
        args: [--fix, --exit-non-zero-on-fix]
```

- No configuration is technically required as ruff is compatible with Black out-of-the-box, as long as the line-length setting is consistent between the two; which by default is 88 characters; this PyCon 2015 [talk](https://www.youtube.com/watch?v=wf-BqAjZb8M&t=260s) explains why 90-ish character line-lengths should be considered.
- Lastly, `pre-commit install` will install the git hooks in `.git/` directory of your project

## Running the pre-commit hooks

You can now run `pre-commit run --all-files` to run black and ruff on all the files in the project. Consider running this command in CI too; as precommit hooks can be ignored using `--no-verify` when commiting.

You can omit the `--all-files` flag to run the pre-commit hooks on staged files in git; just like what will happen on committing files. Ruff will flag any error(s) on attempting to commit; giving you the opportunity to make the changes; re-stage the file(s) and commit. 

Job done!
