---
title: "Software dependencies"
teaching: 10
exercises: 45
editor_options:
  markdown:
    wrap: 72
---

::: questions
-   How can we communicate different versions of software dependencies?
:::

::: objectives
-   Know how to track dependencies of a project
-   Set up an environment and make sure others can reproduce your
    environment
:::

Our codes often depend on other codes that in turn depend on other codes ...

- **Reproducibility**: We can version-control our code with Git but how should we
version-control dependencies?
  How can we capture and communicate dependencies?
- **Dependency hell**: Different codes on the same environment can have conflicting
dependencies.

![From [xkcd - dependency](https://xkcd.com/2347/){target="_blank"}. Another image that might be familiar to some of you working with Python can be found on [xkcd - superfund](https://xkcd.com/1987/){target="_blank"}.](fig/dependency.png){width="60%" alt="An image showing blocks (=codes) depending on each other for stability"}

::: discussion
## Kitchen analogy

- Software <-> recipe
- Data <-> ingredients
- Libraries <-> pots/tools

![Cooking recipe in an unfamiliar language [Midjourney, CC-BY-NC 4.0]](fig/recipe.png){width=50% alt="Cooking recipe in an unfamiliar language"}

![When we create recipes, we often use tools created by others (libraries) [Midjourney, CC-BY-NC 4.0]](fig/libraries.png){width=50% alt="Kitchen with few open cooking books"}

:::

## Tools and what problems they try to solve

**Conda, Anaconda, pip, virtualenv, Pipenv, pyenv, Poetry, requirements.txt,
environment.yml, renv**, ..., these tools try to solve the following problems:

- **Defining a specific set of dependencies**, possibly with well defined versions
- **Installing those dependencies** mostly automatically
- **Recording the versions** for all dependencies
- **Isolate environments**
  - On your computer for projects so they can use different software
  - Isolate environments on computers with many users (and allow self-installations)
- Using **different Python/R versions** per project
- Provide tools and services to **share packages**

Isolated environments are also useful because they help you make sure
that you know your dependencies!

**If things go wrong, you can delete and re-create** - much better
than debugging. The more often you re-create your environment, the
more reproducible it is.


::: challenge
## Dependencies-1: Time-capsule of dependencies

Situation: 3 students (A, B, C) wrote a code that depends on a couple of libraries.
They uploaded their projects to GitHub. We now travel 3 years into the future
and find their GitHub repositories and try to re-run their code before adapting
it.

Answer in the collaborative document:

- Which version do you expect to be easiest to re-run? Why?
- What problems do you anticipate in each solution?

::: group-tab
### Python

**A**:
You find various library imports across the code. The README file lists some
of the main libraries that were used but does not mention versions.

**B**:
You find a `requirements.txt` file with:
```
scipy
numpy
sympy
click
git+https://github.com/someuser/someproject.git@main
git+https://github.com/anotheruser/anotherproject.git@main
```

**C**:
You find a `requirements.txt` file with:
```
scipy==1.3.1
numpy==1.16.4
sympy==1.4
click==7.0
someproject==1.2.3
git+https://github.com/anotheruser/anotherproject.git@sometag
```

### R
**A**:
You find various `library()` or `require()` calls across the code. The README
file lists a few of the libraries that were used but does not mention versions.

**B**:
You find a [DESCRIPTION file](https://r-pkgs.org/description.html){target="_blank"} which contains:
```
Imports:
dplyr,
tidyr
```
In addition you find these:
```r
remotes::install_github("someuser/someproject@main")
remotes::install_github("anotheruser/anotherproject@main")
```

**C**:
You find a [DESCRIPTION file](https://r-pkgs.org/description.html){target="_blank"} which contains:
```
Imports:
dplyr (== 1.0.0),
tidyr (== 1.1.0),
someproject (== 1.2.3),
remotes::install_github("anotheruser/anotherproject@sometag")
```
:::

::: solution
**A**: If there is no standard file to look for, it might become very difficult
for us to create the software environment required to run the software. At
least we know some of the libraries. For any missing dependencies, it will be
tedious to collect them one by one. And even then you still don't know which
versions were used.

**B**: Having a standard file listing dependencies is definitely better
than nothing. However, if the versions are not specified, you or someone
else might run into problems with dependencies, deprecated features,
changes in package APIs, etc. Versions specified as Git branches may not be
much better: branches such as `main` are still a moving target.

**C**: In this case exact versions of all dependencies are specified and one
can recreate the software environment required for the project. One problem
with the dependencies that come from GitHub is that they might have disappeared
(what if their authors deleted these repositories?). Besides that, version
numbers give a better idea of progress compared to arbitrary tags. From a
simple list, there is no clear ordering between two tags `with-some-feature` or
`used-for-this-paper`, while version `2.0.0` is obviously newer than `1.2.3`.

:::

:::

::: challenge
## (Optional) Further discussions for specifying dependencies
1. How would it differ if student **A** did not specify any dependencies in the
README at all? Or if a complete list of dependencies was given?
2. What would be the difference between `someuser/someproject@d7b2c7e` versus
`someuser/someproject@main` being listed as a dependency?

:::

::: solution
1. Any dependencies listed in the README are still helpful, so listing none at
all when no other information exists would be worse. Specifying a full list is
therefore better. However, a README can easily be outdated, so there is no
guarantee that this list is up-to-date or complete.
2. The `d7b2c7e` instead of `main` is a git commit hash, which is at least a
consistent point in the history of the code. Installing a specific commit will
give the same result, even if the development of the project has continued on
the `main` branch. The only downside is that a commit hash has no meaning to
us as humans looking at it. To clarify the meaning of a particular commit, it
would be helpful to make a git tag of it.

:::


::: challenge
## Dependencies-2: Create a time-capsule for the future

Now we will demo creating our own time-capsule and share it with the future
world. If we asked you now which dependencies your project is using, what would
you answer? How would you find out? And how would you communicate this
information?

::: group-tab
### Python
Try this in your own project:
```console
$ pip freeze > requirements.txt
```

Have a look at the generated file and discuss what you see.

In future you can re-create this environment with:
```console
$ pip install -r requirements.txt
```

If you want to learn more about virtual environments in Python, head over to the
[Carpentries Intermediate Research Software Development Skills (Python) ](https://carpentries-incubator.github.io/python-intermediate-development/12-virtual-environments/index.html#creating-virtual-environments-using-venv){target="_blank"}
lesson.

### R
This example uses renv.

First initialize renv (install the package if needed) using `renv::init()`.
Then try to "save" and "load" the state of your project library using
`renv::snapshot()` and `renv::restore()`.
See also: <https://rstudio.github.io/renv/articles/renv.html#reproducibility>{target="_blank"}

If you want to learn more about using `renv` in R, head over to the
[Introduction to Reproducible Publications with RStudio](https://carpentries-incubator.github.io/reproducible-publications-quarto/03-collaboration/05-renv/index.html){target="_blank"}
lesson.

:::

:::


::: challenge
## Uploading your requirements.txt or renv files to GitHub
Follow these steps to add the files in which you recorded your dependencies to GitHub:

::: group-tab
### RStudio
1. Add your changed files by clicking on 'Staged' (share not only the lock file, but also the .RProfile
and activate.R files needed to recreate the environment).
2. Commit your changes by adding a commit message (e.g., "Add dependencies") and clicking on 'Commit'.
3. Push your changes to GitHub by clicking on 'Push'.

### Visual Studio Code
1. Add your changed files by clicking on the '+' next to 'Changes' or next to the individual files (requirements.txt).
2. Commit your changes by adding a commit message (e.g., "Add dependencies") and clicking on 'Commit'.
3. Push your changes to GitHub by clicking on the blue 'Sync Changes' button.

:::

:::


This episode is based on the [Code Refinery](https://coderefinery.github.io/reproducible-research/dependencies/#){target="_blank"}
Reproducible Research lesson about dependencies.


::: keypoints

- Recording dependencies with versions can make it easier for the next person to execute your code
- There are many tools to record dependencies

:::
