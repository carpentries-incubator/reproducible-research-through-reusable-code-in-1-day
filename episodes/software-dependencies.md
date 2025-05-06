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

Situation: 5 students (A, B, C, D, E) wrote a code that depends on a couple of libraries.
They uploaded their projects to GitHub. We now travel 3 years into the future
and find their GitHub repositories and try to re-run their code before adapting
it.

Answer in the collaborative document:

- Which version do you expect to be easiest to re-run? Why?
- What problems do you anticipate in each solution?

::: group-tab
### Python virtualenv

**A**:
You find a couple of library imports across the code but that's it.

**B**:
The README file lists which libraries were used but does not mention
any versions.

**C**:
You find a `requirements.txt` file with:
```
scipy
numpy
sympy
click
python
git+https://github.com/someuser/someproject.git@master
git+https://github.com/anotheruser/anotherproject.git@master
```

**D**:
You find a `requirements.txt` file with:
```
scipy==1.3.1
numpy==1.16.4
sympy==1.4
click==7.0
python==3.8
git+https://github.com/someuser/someproject.git@d7b2c7e
git+https://github.com/anotheruser/anotherproject.git@sometag
```

**E**:
You find a `requirements.txt` file with:
```
scipy==1.3.1
numpy==1.16.4
sympy==1.4
click==7.0
python==3.8
someproject==1.2.3
anotherproject==2.3.4
```

### R
**A**:
You find a couple of `library()` or `require()` calls across the code but that's it.

**B**:
The README file lists which libraries were used but does not mention
any versions.

**C**:
You find a [DESCRIPTION file](https://r-pkgs.org/description.html){target="_blank"} which contains:
```
Imports:
dplyr,
tidyr
```
In addition you find these:
```r
remotes::install_github("someuser/someproject@master")
remotes::install_github("anotheruser/anotherproject@master")
```

**D**:
You find a [DESCRIPTION file](https://r-pkgs.org/description.html){target="_blank"} which contains:
```
Imports:
dplyr (== 1.0.0),
tidyr (== 1.1.0)
```
In addition you find these:
```r
remotes::install_github("someuser/someproject@d7b2c7e")
remotes::install_github("anotheruser/anotherproject@sometag")
```

**E**:
You find a [DESCRIPTION file](https://r-pkgs.org/description.html){target="_blank"} which contains:
```
Imports:
dplyr (== 1.0.0),
tidyr (== 1.1.0),
someproject (== 1.2.3),
anotherproject (== 2.3.4)
```
:::

::: solution
**A**: It will be tedious to collect the dependencies one by one. And after
the tedious process you will still not know which versions they have used.

**B**: If there is no standard file to look for and look at and it might
become very difficult for to create the software environment required to
run the software. But at least we know the list of libraries. But we don't
know the versions.

**C**: Having a standard file listing dependencies is definitely better
than nothing. However, if the versions are not specified, you or someone
else might run into problems with dependencies, deprecated features,
changes in package APIs, etc.

**D** and **E**: In both these cases exact versions of all dependencies are
specified and one can recreate the software environment required for the
project. One problem with the dependencies that come from GitHub is that
they might have disappeared (what if their authors deleted these
repositories?).

**E** is slightly preferable because version numbers are easier to understand than Git
commit hashes or Git tags.

:::

:::


::: challenge
## Dependencies-2: Create a time-capsule for the future

Now we will demo creating our own time-capsule and share it with the future
world. If we asked you now which dependencies your project is using, what would
you answer? How would you find out? And how would you communicate this
information?

::: group-tab
### Python virtualenv
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
