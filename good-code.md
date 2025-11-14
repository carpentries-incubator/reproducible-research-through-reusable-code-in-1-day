---
title: "Coding conventions and modular coding"
teaching: 15
exercises: 60
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why should you follow software code style conventions?
- What code style conventions can you use in Python and R?
- How can nested code be targeted and improved through modularization?
- How can I write a new function in R?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Know how to write readable code
- Know how to write modular code

::::::::::::::::::::::::::::::::::::::::::::::::

## Coding conventions and style guides

Readable code - for others and our future selves - should be descriptive, cleanly 
and consistently formatted, and use sensible, descriptive names for variables, functions 
and modules.  

In order to help us format our code, we can follow guidelines known as a style guide. 
A style guide is a set of conventions that we agree upon with our colleagues
or community, to ensure that people produce code which looks similar in style.
The most important thing about a style guide is that it provides consistency, making 
code easier to read and also easier to write - because you need to make fewer decisions.

::: challenge

::: tab
### Python style guide
Head over to [this lesson about the Python style guide](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions.html#python-coding-style-guide){target="_blank"}.  

Then take a look at (a part of) your own Python script, and identify where the guidelines 
have not been followed. Check the following:

- [Indentation](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions#indentation){target="_blank"}
- [Whitespace in Expressions and Statements](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions#whitespace-in-expressions-and-statements){target="_blank"}
- [Naming conventions](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions#naming-conventions){target="_blank"}
- [Comments](https://carpentries-incubator.github.io/python-intermediate-development/15-coding-conventions#comments){target="_blank"}

Fix the discovered inconsistencies and commit them to your working branch on GitHub.

### R (Tidyverse) style guide
Head over to [the Tidyverse style guide](https://style.tidyverse.org/){target="_blank"}.  

Then take a look at (a part of) your own R script, and identify where the guidelines 
have not been followed. Check the following:

- [Indentation](https://style.tidyverse.org/functions.html#multi-line-function-definitions){target="_blank"}
- [Spacing](https://style.tidyverse.org/syntax.html#spacing){target="_blank"}
- [File](https://style.tidyverse.org/files.html){target="_blank"} and [object](https://style.tidyverse.org/syntax.html){target="_blank"} 
naming conventions
- [Comments](https://style.tidyverse.org/functions.html#comments){target="_blank"}

Fix the discovered inconsistencies and commit them to your working branch on GitHub.
You can use the [styler](https://styler.r-lib.org/){target="_blank"} (with RStudio add-in) and [lintr](https://github.com/r-lib/lintr){target="_blank"}
packages to (re-)style your code.

:::

:::

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
