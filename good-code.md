---
title: "Coding conventions and modular coding"
teaching: 15
exercises: 60
---

:::::::::::::::::::::::::::::::::::::: questions

- Why should you follow software code style conventions?
- How can formatters and linters help you with this in Python and R?
- How can nested code be targeted and improved through modularization?
- How can I write a new function in R?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Know how to write readable code
- Know how to write modular code

::::::::::::::::::::::::::::::::::::::::::::::::

## Coding formatting and linting

Readable code - for others and our future selves - should be descriptive, cleanly
and consistently formatted, and use sensible, descriptive names for variables, functions
and modules. Furthermore, our code should be efficient and well designed.

Programs called formatters and linters can help us with the above. What do they
do and how do they differ?

### Formatters

With a light touch, formatters ensure the code adheres to standard style guides without altering
functionality. A style guide is a set of conventions that we agree upon with our
colleagues or community, to ensure that people produce code which looks similar
in style. For examples, check out the [PEP 8 Style Guide](https://peps.python.org/pep-0008/) or
the [Tidyverse style guide](https://style.tidyverse.org/) for Python and R, respectively.

Good, consistent formatting makes the code easier to read and can prevent merge
conflicts.

### Linters

The work of "linters" is a bit more heavy-handed. These programs can check your code
for common programming errors, convoluted syntax, unnecessary complexity, unused code,
performance bottlenecks and other violations of best practices. Often they can fix the
issues they encounter, or suggest appropriate improvements otherwise.

### Naming conventions

Naming things is hard. With their names, we want to convey as much meaning as
possible in a limited number of characters. A good name follows the style
conventions of the language, and provides useful meaning in its context.
Linters will help you with the style aspect, since they will complain if you
don't follow the style guide of your language.

Making your names meaningful is the hardest part. Since short names are usually
preferred over long names, a common mistake is making the names so short they
don't have enough meaning without extra context. For example, what would
variables `a`, `t`, or `x` be? What do you think a function called `run` or
`process` does? On the other hand, `time_in_hours_since_last_restaurant_visit`
is obviously too verbose. Working in the limited context of small functions or
dedicated classes, a few words should usually be enough: e.g.,
`hours_since_visit`. Getting this right takes practice, trial and error. Read
other people's code for inspiration and ask for feedback on yours!

Some generic advice for naming things:

1. Follow the style guide for your language/codebase
2. Variables and classes are nouns, functions are verbs
3. Avoid single letters or abbreviations if possible
4. When in doubt, it is better to be overly specific than too general
5. Watch for keywords like `and` to indicate that a function can be split
6. Ask what meaning others get from your names. What would they suggest instead?


::::::::::::::::::::::::::::::::::::: instructor

For the exercises, focus on one or two files instead of a whole project. The
goals is to learn the tools, not necessarily to improve everything just yet.

::::::::::::::::::::::::::::::::::::::::::::::::

### Improving your code

::: challenge

Install and use a formatter and a linter to improve the style of your code.

::: tab
### Python
[The program `ruff`](https://github.com/astral-sh/ruff) can both format _and_ lint
Python code. [Install `ruff`](https://docs.astral.sh/ruff/installation/) from PyPI
or conda. Don't forget to add it to your `requirements.txt`, `pyproject.toml` or
whichever file you use to define your dependencies.

**Formatting**

First, use the formatter. Note that the use without the `--check` or `--diff`
flag `ruff` automatically changes your file. This is the default, because
formatting does not change the behaviour of your code.

```bash
# Check for formatting
ruff format --check

# Show what formatting fixes can be applied, without writing anything
ruff format --diff

# Fix formatting, if desired
ruff format
```

Do you agree with the default choices `ruff` made? You can
[configure](https://docs.astral.sh/ruff/tutorial/#configuration) `ruff` to follow
your choices if you need to, but be aware that the defaults were chosen for a reason.

**Linting**

Next, try out the linter. While fixing formatting is usually harmless, linting
fixes change your code on a deeper level. By default, `ruff check` only advises
you. To automatically apply the linting, you need an explicit `--fix` flag. This
is because linting can touch the functionality of your code, so make sure to
review the changes `ruff check` makes using e.g. `ruff check --diff`.

```bash
# Check for linting
ruff check

# Show what linting fixes can be applied, without writing anything
ruff check --diff

# Fix linting, if desired
ruff check --fix
```

What is your opinion on the linting suggestions? Again, you can
[configure](https://docs.astral.sh/ruff/tutorial/#configuration) the details `ruff`
pays attention to when linting. Did you learn something new about the Python language?

### R

The standard option for [formatting R code is `styler`](https://styler.r-lib.org/), for [linting it's `lintr`](https://lintr.r-lib.org/).

```R
# Install the formatter and linter.
install.packages(c("styler", "lintr"))
```

If the installation fails due to a missing `libxml-2.0` library, install it first (it's called `libxml2-dev` in Ubuntu) and re-run the installation.

**Formatting**

You will notice that both new packages are listed under the "Addins" menu in RStudio. Open an R file and use

```
Addins ➜ STYLER ➜ "Style active file".
```

Do you agree with the default choices that `styler` made? You can [configure](https://styler.r-lib.org/articles/styler.html#invasiveness) `styler` to follow your choices if you need to, but be aware that the defaults were chosen for a reason. You can also configure it under

```
Addins ➜ STYLER ➜ "Set style".
```

**Linting**

Next, try out the linter with

```
Addins ➜ LINTR ➜ "Lint current file".
```

While fixing formatting is usually harmless, linting fixes change your code on a deeper level. Make sure to review the changes `lintr` makes.

What is your opinion on the linting suggestions? Again, you can [configure](https://lintr.r-lib.org/#usage) the details `lintr` pays attention to when linting. Did you learn something new about the R language?

**Further reading: R Coding Style**

https://www.datanovia.com/en/blog/r-coding-style-best-practices/<br>
https://rfortherestofus.com/2024/03/styler-package

:::

:::

### (Optional) Git pre-commit hooks

So far, formatting and linting were conscious choices: you have to remember to execute
them yourself every once in a while. A more robust approach would be to take away this
mental load and automate linting and formatting. This can be achieved through "git hooks",
which are a set of scripts `git` can run every time a certain action is performed. Here
we have a look at "pre-commit hooks" that check your code changes _before_ you commit them.

::: challenge

The amount of git pre-commit hook scripts can grow rather large on
bigger projects. `pre-commit` manages your commit hooks and helper programs in a
declarative way and makes them easy to share between collaborators.

Use a `git` pre-commit hook to run formatters and linters every time before a `git commit`.

::: tab
### Python
Install [pre-commit](https://pre-commit.com/) and add it to your `requirements.txt` or
`pyproject.toml`.

Create a `pre-commit` config file named `.pre-commit-config.yaml`.

```yaml
repos:
- repo: https://github.com/astral-sh/ruff-pre-commit
  # Ruff version.
  rev: v0.14.8
  hooks:
    # Run the linter.
    - id: ruff-check
      # Possible choices: [ python, pyi, jupyter ]
      # Here we exclude Jupyter notebooks
      types_or: [ python, pyi ]

      # Comment _out_ to only check, not fix
      args: [ --fix ]

    # Run the formatter.
    - id: ruff-format

      # Comment _in_ to only check, not fix
      # args: [ --check ]

      # Possible choices: [ python, pyi, jupyter ]
      # Here we exclude Jupyter notebooks
      types_or: [ python, pyi ]
```

If you would want to run additional checks, you need to add a new `- repo:` entry
to the `pre-commit` config file.

Make sure to add and commit this file to your `git` repository, so your collaborators
will use the exact same configurations and versions.

```bash
git add .pre-commit-config.yaml
git commit -m "add pre-commit hook for formatting and linting"
```

Install the new git hook.

```bash
pre-commit install
```

You can test your script by executing it manually.

```bash
pre-commit run --all-files
```

For updating your hooks to the latest version, run

```bash
pre-commit autoupdate
```

and make sure to add and commit your updated config file.

### R

Install the package `precommit` and initialize it.

⚠️ This package is only supported on operating systems that are also officially
supported by R. Please check the [R Download page](https://cran.rstudio.org/) which
ones are eligible. Non long-term-stable (LTS) Ubuntu distributions, for example, are
not. Installing and running `precommit` on non-supported operating systems will
probably require extra manual work.

```R
install.packages("precommit")
precommit::use_precommit()
```

RStudio will open the `.pre-commit-config.yaml` file for you to review. It will look
something like this:

```yaml
# All available hooks: https://pre-commit.com/hooks.html
# R specific hooks: https://github.com/lorenzwalthert/precommit
repos:
-   repo: https://github.com/lorenzwalthert/precommit
    rev: v0.4.3.9017
    hooks:
    -   id: style-files
        args: [--style_pkg=styler, --style_fun=tidyverse_style]
    -   id: spell-check
        exclude: >
          (?x)^(
          .*\.[rR]|
          .*\.feather|
          .*\.jpeg|
          .*\.pdf|
          .*\.png|
          .*\.py|
          .*\.RData|
          .*\.rds|
          .*\.Rds|
          .*\.Rproj|
          .*\.sh|
          (.*/|)\.gitignore|
          (.*/|)\.gitlab-ci\.yml|
          (.*/|)\.lintr|
          (.*/|)\.pre-commit-.*|
          (.*/|)\.Rbuildignore|
          (.*/|)\.Renviron|
          (.*/|)\.Rprofile|
          (.*/|)\.travis\.yml|
          (.*/|)appveyor\.yml|
          (.*/|)NAMESPACE|
          (.*/|)renv/settings\.dcf|
          (.*/|)renv\.lock|
          (.*/|)WORDLIST|
          \.github/workflows/.*|
          data/.*|
          )$
    -   id: lintr
    -   id: readme-rmd-rendered
    -   id: parsable-R
    -   id: no-browser-statement
    -   id: no-debug-statement
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v6.0.0
    hooks:
    -   id: check-added-large-files
        args: ['--maxkb=200']
    -   id: end-of-file-fixer
        exclude: '\.Rd'
-   repo: https://github.com/pre-commit-ci/pre-commit-ci-config
    rev: v1.6.1
    hooks:
    # Only required when https://pre-commit.ci is used for config validation
    -   id: check-pre-commit-ci-config
-   repo: local
    hooks:
    -   id: forbid-to-commit
        name: Don't commit common R artifacts
        entry: Cannot commit .Rhistory, .RData, .Rds or .rds.
        language: fail
        files: '\.(Rhistory|RData|Rds|rds)$'
        # `exclude: <regex>` to allow committing specific files

ci:
    autoupdate_schedule: monthly
```

You can comment out `repo` or `id` stanzas if you don't want them, or add new
ones if you want more checks to happen before you commit files.

<!-- Head over to [the Tidyverse style guide](https://style.tidyverse.org/){target="_blank"}.

Then take a look at (a part of) your own R script, and identify where the guidelines
have not been followed. Check the following:

- [Indentation](https://style.tidyverse.org/functions.html#multi-line-function-definitions){target="_blank"}
- [Spacing](https://style.tidyverse.org/syntax.html#spacing){target="_blank"}
- [File](https://style.tidyverse.org/files.html){target="_blank"} and [object](https://style.tidyverse.org/syntax.html){target="_blank"}
naming conventions
- [Comments](https://style.tidyverse.org/functions.html#comments){target="_blank"}

Fix the discovered inconsistencies and commit them to your working branch on GitHub.
You can use the [styler](https://styler.r-lib.org/){target="_blank"} (with RStudio add-in) and [lintr](https://github.com/r-lib/lintr){target="_blank"}
packages to (re-)style your code. -->

https://www.r-bloggers.com/2022/09/enforcing-style-in-an-r-project/

:::

⚠️ Failed pre-commit checks will also fail the commit! Make sure to resolve the issues
- be it fixing the code, or excluding certain lines from being checked - and commit
again.

:::


### Further reading: CI/CD

We went from running formatting and linting locally to automating the checks for
every commit. This still leaves a margin for error since your collaborators will
need to set up the git hooks first. The next line of defense against messy contributions
is CI/CD (Continuous Integration / Continuous Delivery).

It goes beyond the scope of this module, but you can set up your remote repository
such that every push (or pull/merge request) triggers a set of checks. For GitHub it
is named [GitHub Actions](https://docs.github.com/en/actions), while GitLab just calls
it [CI/CD](https://docs.gitlab.com/ci/). It is useful beyond just code style; other
common usecases include automated testing (even on different platforms, like Linux, Windows
or MacOS), compilation and packaging, deployment, benchmarking, security checks...
There is a whole [marketplace](https://github.com/marketplace) for reusing CI/CD
recipes.

Usually the tools you use will supply instructions on how to run them in this automated way.
Check out [`ruff` integrations](https://docs.astral.sh/ruff/integrations/) for Python,
or [`lintr` integrations](https://github.com/r-lib/lintr/?tab=readme-ov-file#setting-up-github-actions)
and [`styler` integrations](https://github.com/r-lib/actions/tree/v2-branch/examples#style-package) for R.
Both [rely on the `usethis`](https://usethis.r-lib.org/reference/use_github_action.html) package.

## Modular coding

### What is modularity?
Modularity refers to the practice of building software from smaller, self-contained,
and independent elements. Each element is designed to handle a specific set of tasks,
contributing to the overall functionality of the system.

Modular coding is explained in more detail in [these slides](https://esciencecenter-digital-skills.github.io/digital-skills-slides/modules/good-practices-lesson/modular-code-slides){target="_blank"}.

### Writing functions
One of the best ways to improve your code and to make it more modular is to write functions.
Functions allow you to automate common tasks in a more powerful and general way than
copy-and-pasting. Writing a function has four big advantages over using copy-and-paste:

1.  You can give a function an evocative name that makes your code easier to understand.

2.  As requirements change, you only need to update code in one place, instead of many.

3.  You eliminate the chance of making incidental mistakes when you copy and paste (i.e.
updating a variable name in one place, but not in another).

4.  It makes it easier to reuse work from project-to-project, increasing your productivity
over time.

A good rule of thumb is to consider writing a function whenever you’ve copied and pasted a
block of code more than twice (i.e. you now have three copies of the same code).

### Defining a function

::: tab

### Defining a function in R

Let's open a new R script file and call it functions-lesson.R.

The general structure of a function is:

```r
my_function <- function(parameters) {
  # perform action
  # return value
}
```

Let's define a function `fahr_to_kelvin()` that converts temperatures from
Fahrenheit to Kelvin:

```r
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5 / 9)) + 273.15
  return(kelvin)
}
```

We define `fahr_to_kelvin()` by assigning it to the output of `function`. The
list of argument names are contained within parentheses.   Next, the
body of the function--the
statements that are executed when it runs--is contained within curly braces
(`{}`). The statements in the body are indented by two spaces. This makes the
code easier to read but does not affect how the code operates.

It is useful to think of creating functions like writing a cookbook. First you define
the "ingredients" that your function needs. In this case, we only need one ingredient
to use our function: "temp". After we list our ingredients, we then say what we will do
with them, in this case, we are taking our ingredient and applying a set of mathematical
operators to it.

When we call the function, the values we pass to it as arguments are assigned to
those variables so that we can use them inside the function. Inside the
function, we use a [return
statement](https://swcarpentry.github.io/r-novice-gapminder/reference.html#return-statement){target="_blank"}
to send a result back to whoever asked for it.

Let's try running our function.
Calling our own function is no different from calling any other function:

```r
# freezing point of water
fahr_to_kelvin(32)
```

```output
[1] 273.15
```

```r
# boiling point of water
fahr_to_kelvin(212)
```
```output
[1] 373.15
```

### Defining a function in Python
Let's open a new Python script file and call it `functions-lesson.py`

The general structure of a function is:

```python
def my_function(parameters):
  # perform action
  # return value
```

Let's define a function `fahr_to_kelvin()` that converts temperatures from
Fahrenheit to Kelvin:

```python
def fahr_to_kelvin(temp):
    kelvin = ((temp - 32) * (5 / 9)) + 273.15
    return kelvin
```

We define `fahr_to_kelvin()` by using the `def` keyword. The
list of argument names are contained within parentheses.

Next, the
body of the function--the
statements that are executed when it runs--is indicated with indentation.
The statements in the body are indented by four spaces.

It is useful to think of creating functions like writing a cookbook. First you define
the "ingredients" that your function needs. In this case, we only need one ingredient
to use our function: "temp". After we list our ingredients, we then say what we will do
with them, in this case, we are taking our ingredient and applying a set of mathematical
operators to it.

When we call the function, the values we pass to it as arguments are assigned to
those variables so that we can use them inside the function. Inside the
function, we use a return statement
to send a result back to whoever asked for it.

Let's try running our function.
Calling our own function is no different from calling any other function:

```python
# freezing point of water
fahr_to_kelvin(32)
```

```output
[1] 273.15
```

```python
# boiling point of water
fahr_to_kelvin(212)
```
```output
[1] 373.15
```

:::

::::::::::::::::::::::::::::::::::::: instructor

Again, for the next exercise, focus on one or two files first. Students who
need a challenge can choose to improve more files.

::::::::::::::::::::::::::::::::::::::::::::::::

::: challenge
## Challenge: Identify code that can be put in a function
In your own project: identify code that would fit better in a function.
Try to look for pieces of code that you repeat throughout your project.

[Create an issue in your project](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-an-issue){target="_blank"}
for each possible function that you find. (Actually implementing the function is beyond the scope of this workshop).

GitHub issues are a good way to track your progress and to-do list.
As well as a way for others to signal issues with your code.
:::

## (Optional) Modularity in Python

::: challenge

Carefully review the following code snippet:

```python
def convert_temperature(temperature, unit):
    if unit == "F":
        # Convert Fahrenheit to Celsius
        celsius = (temperature - 32) * (5 / 9)
        if celsius < -273.15:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Kelvin
            kelvin = celsius + 273.15
            if kelvin < 0:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                fahrenheit = (celsius * (9 / 5)) + 32
                if fahrenheit < -459.67:
                    # Invalid temperature, below absolute zero
                    return "Invalid temperature"
                else:
                    return celsius, kelvin
    elif unit == "C":
        # Convert Celsius to Fahrenheit
        fahrenheit = (temperature * (9 / 5)) + 32
        if fahrenheit < -459.67:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Kelvin
            kelvin = temperature + 273.15
            if kelvin < 0:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                return fahrenheit, kelvin
    elif unit == "K":
        # Convert Kelvin to Celsius
        celsius = temperature - 273.15
        if celsius < -273.15:
            # Invalid temperature, below absolute zero
            return "Invalid temperature"
        else:
            # Convert Celsius to Fahrenheit
            fahrenheit = (celsius * (9 / 5)) + 32
            if fahrenheit < -459.67:
                # Invalid temperature, below absolute zero
                return "Invalid temperature"
            else:
                return celsius, fahrenheit
    else:
        return "Invalid unit"
```

Refactor the code by extracting functions without altering its functionality.

- What functions did you create?
- What strategies did you use to identify them?

Share your answers in the collaborative document.

:::: solution

## Solution 1 - Basic

```python
def celsius_to_fahrenheit(celsius):
    """
    Converts a temperature from Celsius to Fahrenheit.

    Args:
        celsius (float): The temperature in Celsius.

    Returns:
        float: The temperature in Fahrenheit.
    """
    return (celsius * (9 / 5)) + 32


def fahrenheit_to_celsius(fahrenheit):
    """
    Converts a temperature from Fahrenheit to Celsius.

    Args:
        fahrenheit (float): The temperature in Fahrenheit.

    Returns:
        float: The temperature in Celsius.
    """
    return (fahrenheit - 32) * (5 / 9)


def celsius_to_kelvin(celsius):
    """
    Converts a temperature from Celsius to Kelvin.

    Args:
        celsius (float): The temperature in Celsius.

    Returns:
        float: The temperature in Kelvin.
    """
    return celsius + 273.15


def kelvin_to_celsius(kelvin):
    """
    Converts a temperature from Kelvin to Celsius.

    Args:
        kelvin (float): The temperature in Kelvin.

    Returns:
        float: The temperature in Celsius.
    """
    return kelvin - 273.15


def check_temperature_validity(temperature, unit):
    """
    Checks if a temperature is valid for a given unit.

    Args:
        temperature (float): The temperature to check.
        unit (str): The unit of the temperature. Must be "C", "F", or "K".

    Returns:
        bool: True if the temperature is valid, False otherwise.
    """
    abs_zero = {"C": -273.15, "F": -459.67, "K": 0}
    if temperature < abs_zero[unit]:
        return False
    return True


def check_unit_validity(unit):
    """
    Checks if a unit is valid.

    Args:
        unit (str): The unit to check. Must be "C", "F", or "K".

    Returns:
        bool: True if the unit is valid, False otherwise.
    """
    if not unit in ["C", "F", "K"]:
        return False
    return True


def convert_temperature(temperature, unit):
    """
    Converts a temperature from one unit to another.

    Args:
        temperature (float): The temperature to convert.
        unit (str): The unit of the temperature. Must be "C", "F", or "K".

    Returns:
        tuple: A tuple containing the converted temperature in Celsius and Kelvin units.

    Raises:
        ValueError: If the unit is not "C", "F", or "K".
        ValueError: If the temperature is below absolute zero for the given unit.

    Examples:
        >>> convert_temperature(32, "F")
        (0.0, 273.15)
        >>> convert_temperature(0, "C")
        (32.0, 273.15)
        >>> convert_temperature(273.15, "K")
        (0.0, -459.67)
    """
    if not check_unit_validity(unit):
        raise ValueError("Invalid unit")
    if not check_temperature_validity(temperature, unit):
        raise ValueError("Invalid temperature")
    if unit == "F":
        celsius = fahrenheit_to_celsius(temperature)
        kelvin = celsius_to_kelvin(celsius)
        return celsius, kelvin
    if unit == "C":
        fahrenheit = celsius_to_fahrenheit(temperature)
        kelvin = celsius_to_kelvin(temperature)
        return fahrenheit, kelvin
    if unit == "K":
        celsius = kelvin_to_celsius(temperature)
        fahrenheit = celsius_to_fahrenheit(celsius)
        return celsius, fahrenheit

if __name__ == "__main__":
    print(convert_temperature(0, "C"))
    print(convert_temperature(0, "F"))
    print(convert_temperature(0, "K"))
    print(convert_temperature(-500, "K"))
    print(convert_temperature(-500, "C"))
    print(convert_temperature(-500, "F"))
    print(convert_temperature(-500, "B"))
```

::::
:::: solution

## Solution 2 - Advanced

```python
class TemperatureConverter:
    """
    A class for converting temperatures between Celsius, Fahrenheit, and Kelvin.
    """

    def __init__(self):
        """
        Initializes the TemperatureConverter object with a dictionary of absolute zero temperatures for each unit.
        """
        self.abs_zero = {"C": -273.15, "F": -459.67, "K": 0}

    def celsius_to_fahrenheit(self, celsius):
        """
        Converts a temperature from Celsius to Fahrenheit.

        Args:
            celsius (float): The temperature in Celsius.

        Returns:
            float: The temperature in Fahrenheit.
        """
        return (celsius * (9 / 5)) + 32

    def fahrenheit_to_celsius(self, fahrenheit):
        """
        Converts a temperature from Fahrenheit to Celsius.

        Args:
            fahrenheit (float): The temperature in Fahrenheit.

        Returns:
            float: The temperature in Celsius.
        """
        return (fahrenheit - 32) * (5 / 9)

    def celsius_to_kelvin(self, celsius):
        """
        Converts a temperature from Celsius to Kelvin.

        Args:
            celsius (float): The temperature in Celsius.

        Returns:
            float: The temperature in Kelvin.
        """
        return celsius + 273.15

    def kelvin_to_celsius(self, kelvin):
        """
        Converts a temperature from Kelvin to Celsius.

        Args:
            kelvin (float): The temperature in Kelvin.

        Returns:
            float: The temperature in Celsius.
        """
        return kelvin - 273.15

    def check_temperature_validity(self, temperature, unit):
        """
        Checks if a given temperature is valid for a given unit.

        Args:
            temperature (float): The temperature to check.
            unit (str): The unit to check the temperature against.

        Returns:
            bool: True if the temperature is valid for the unit, False otherwise.
        """
        if temperature < self.abs_zero[unit]:
            return False
        return True

    def check_unit_validity(self, unit):
        """
        Checks if a given unit is valid.

        Args:
            unit (str): The unit to check.

        Returns:
            bool: True if the unit is valid, False otherwise.
        """
        if unit not in ["C", "F", "K"]:
            return False
        return True

    def convert_temperature(self, temperature, unit):
        """
        Converts a temperature from one unit to another.

        Args:
            temperature (float): The temperature to convert.
            unit (str): The unit of the temperature.

        Returns:
            tuple: A tuple containing the converted temperature in the other two units.
        """
        if not self.check_unit_validity(unit):
            raise ValueError("Invalid unit")
        if not self.check_temperature_validity(temperature, unit):
            raise ValueError("Invalid temperature")
        if unit == "F":
            celsius = self.fahrenheit_to_celsius(temperature)
            kelvin = self.celsius_to_kelvin(celsius)
            return celsius, kelvin
        if unit == "C":
            fahrenheit = self.celsius_to_fahrenheit(temperature)
            kelvin = self.celsius_to_kelvin(temperature)
            return fahrenheit, kelvin
        if unit == "K":
            celsius = self.kelvin_to_celsius(temperature)
            fahrenheit = self.celsius_to_fahrenheit(celsius)
            return celsius, fahrenheit

if __name__ == "__main__":
    converter = TemperatureConverter()
    print(converter.convert_temperature(0, "C"))
    print(converter.convert_temperature(0, "F"))
    print(converter.convert_temperature(0, "K"))
    print(converter.convert_temperature(-500, "K"))
    print(convert_temperature(-500, "C"))
    print(convert_temperature(-500, "F"))
    print(convert_temperature(0, "X"))
```

::::
:::


## (Optional): Writing good functions in R

::: challenge

## Challenge 1

Write a function called `kelvin_to_celsius()` that takes a temperature in
Kelvin and returns that temperature in Celsius.

Hint: To convert from Kelvin to Celsius you subtract 273.15

:::: solution

## Solution to challenge 1

Write a function called `kelvin_to_celsius` that takes a temperature in Kelvin
and returns that temperature in Celsius

```r
kelvin_to_celsius <- function(temp) {
 celsius <- temp - 273.15
 return(celsius)
}
```

::::

:::

### Combining functions

The real power of functions comes from mixing, matching and combining them
into ever-larger chunks to get the effect we want.

Let's define two functions that will convert temperature from Fahrenheit to
Kelvin, and Kelvin to Celsius:

```r
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5 / 9)) + 273.15
  return(kelvin)
}

kelvin_to_celsius <- function(temp) {
  celsius <- temp - 273.15
  return(celsius)
}
```

:::  challenge

## Challenge 2

Define the function to convert directly from Fahrenheit to Celsius,
by reusing the two functions above (or using your own functions if you
prefer).

::::  solution

## Solution to challenge 2

Define the function to convert directly from Fahrenheit to Celsius,
by reusing these two functions above

```r
fahr_to_celsius <- function(temp) {
  temp_k <- fahr_to_kelvin(temp)
  result <- kelvin_to_celsius(temp_k)
  return(result)
}
```

::::

:::


The Modular coding section is based on the following sources:

- [Modular Code Development](https://esciencecenter-digital-skills.github.io/good-practices-lesson/1-modular-code.html){target="_blank"}
from Good practices in research software development
- [Functions explained](https://swcarpentry.github.io/r-novice-gapminder/10-functions.html){target="_blank"}
from R for Reproducible Scientific Analysis Software Carpentry lesson
- [Functions](https://r4ds.hadley.nz/functions){target="_blank"} chapter from R for Data Science (2e)

:::::::::::::::::::::::::::::::::::::::: keypoints

- Coding conventions help you create more readable code that is easier to reuse and contribute to.
- Consistently formatted code including descriptive variable and function names is easier to read and write
- Software is built from smaller, self-contained elements, each handling specific tasks.
- Modular code enhances robustness, readability, and ease of maintenance.
- Modules can be reused across projects, promoting efficiency.
- Good modules perform limited, defined tasks and have descriptive names.

::::::::::::::::::::::::::::::::::::::::::::::::::
