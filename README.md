# python-semantic-release-poc

## Purpose

This repository aims to provide a brief demonstration of the python-semantic-release package.

## What is semantic release?

Semantic release is an automatic workflow for package releases. Based on the newer commit messages it determines the next version number, generates the changelog, creates a tag and publishes the package.

## Why python-semantic-release?

[python-semantic-release](https://python-semantic-release.readthedocs.io/en/latest/configuration.html#config-upload-to-repository) takes care of the whole process for you, regardless of what CI/CD tool you are currently using. It relies on the repository contributors to use the [Angular commit message style](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits) (by default) to trigger the entire process.

## Okay, but how does it work?

As explained on the official documentation, here is a step-by-step:

### 1. Create a version variable

Create a version variable anywhere in your project, for example, in a `__init__.py` at the root of the project:

```
__version__ = "0.2.0"
```

### 2. Reference the version variable location

In this example, we're going to use the `setup.cfg` file, but you could also add this information to a `pyproject.toml` file:

```
[semantic_release]
version_variable = __init__.py:__version__
```

### 3. Follow a commit message guideline

By default, as mentioned earlier in this guide, `python-semantic-release` uses [Angular commit message style](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits) by default to determine automatically what will be the next software version.

In simple terms, there are a few possible commit types that can be used as a prefix in the message:

* **feat:** A new feature
* **fix:** A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing or correcting existing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation generation

The main ones are `feat` and `fix`, since they will directly count towards the next version.

* **feat** increments the minor version by 1
* **fix** increments the patch version by 1

Now, if a commit is submitting a breaking change, which means, a change that will be incompatible with the previous version (usually when talking about APIs), it is necessary to use the `BREAKING CHANGE:` prefix. Usually a breaking change is followed by a footer explaining what has changed.

Please note that these were merely examples of how the version can be automatically bumped. There might be times when you not necessarily will have a new feature or fix, but still would like to generate a new package version. Use it according to your context

![1.3.2 major.minor.patch](https://miro.medium.com/max/1200/1*D4qTulg6C7nGLltjtAJ5YA.png)

### 4. semantic-release gets triggered

Once all the changes were submitted and your CI is triggered, the semantic release process will start.

There are a few ways to use the package, so please refer to the [official documentation](https://python-semantic-release.readthedocs.io/en/latest/configuration.html#config-upload-to-repository) for more information.

In this example, we have called the `semantic-release publish` command.

Basically, it will follow a few steps:
1. Update the CHANGELOG.md file
2. Bump the software version
3. Create a tag
4. Push changes to git
5. Run the build command (which can be customized)
6. Publish files to the new GitHub Release
7. Publish on Artifactory (not applied on this PoC but can be done)

## Useful links
* [Official documentation](https://python-semantic-release.readthedocs.io/en/latest/configuration.html#config-upload-to-repository)
* [Angular commit message style](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)
* [Configuring your semantic release process](https://python-semantic-release.readthedocs.io/en/latest/configuration.html)