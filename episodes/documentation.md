---
title: Document your research software
teaching: 15
exercises: 30
---

::::::::::::::::::::::::::::::::::::::: objectives

- Know what makes a good README file

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What can I do to make my project more easily understandable?

::::::::::::::::::::::::::::::::::::::::::::::::::

::: instructor
Use [these slides](https://esciencecenter-digital-skills.github.io/digital-skills-slides/modules/good-practices-lesson/documentation-slides){target="_blank"} as
a guidance.

The main purpose of this lesson is to make sure participants understand that DOCUMENTATION IS IMPORTANT. The goal is more to trigger participants 
then to teach them all the different ways one could document a project. It is good to communicate
this (and that this will give more time for the other parts of the workshop).

:::


## Writing good README files
The README file is the first thing a user/collaborator sees. It should include:

- A descriptive project title
- Motivation (why the project exists)
- How to setup
- Copy-pastable quick start code example
- Link or instructions for contributing
- Recommended citation

::: challenge
### Exercise README: Draft or improve a README for your project

Create a new file called README.md in your local project (or improve the README.md file 
for your project).

You can work individually, but you could also discuss whether anything can be improved on 
your neighbour's README file(s).

Think about the user (which can be a future you) of your project, 
what does this user need to know to use or contribute to the project? 
And how do you make your project attractive to use or contribute to?

(Optional): Try the <https://hemingwayapp.com/>{target="_blank"} to analyse your README file 
and make your writing bold and clear.
:::

::: callout
## Uploading your README file to GitHub
Follow these steps to add (the changes to) your README file to GitHub:

::: group-tab
### RStudio
1. Add your changed files by clicking on 'Staged'.
2. Commit your changes by adding a commit message (e.g., "Update README") and clicking on 'Commit'.
3. Push your changes to GitHub by clicking on 'Push'.

### Visual Studio Code
1. Add your changed files by clicking on the '+' next to 'Changes' or next to the individual files (README.md).
2. Commit your changes by adding a commit message (e.g., "Update README") and clicking on 'Commit'.
3. Push your changes to GitHub by clicking on the blue 'Sync Changes' button.

:::

Go to your GitHub repository and refresh the home page to see how the README file 
becomes a sort of landing page for your project.
:::

## (Optional) Other types of documentation.

### In-code documentation

In-code documentation:

- Makes code more understandable
- Explains decisions we made

#### When not to use in-code documentation:
- When the code is self-explanatory
- To replace good variable/function names
- To replace version control
- To keep old (zombie) code around

#### Readable code vs commented code
```python
# convert from degrees celsius to fahrenheit
def convert(d):
    return d * 5 / 9 + 32
```

vs

```python
def celsius_to_fahrenheit(degrees):
    return degrees * 5 / 9 + 32
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Writing good comments - In-code-1: Comments

Let's take a look at two example comments (comments in Python start with `#`):

**Comment A**

```python
  # now we check if temperature is below -50
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Comment B**

```python
  # we regard temperatures below -50 degrees as measurement errors
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Which of these comments is more useful? Can you explain why?**

:::::::::::::::  solution

## Solution

+ **Comment A** describes **what** happens in this piece of code. This can be
    useful for somebody who has never seen Python or a program, but for somebody
    who has, it can feel like a redundant commentary.
+ **Comment B** is probably more useful as it describes **why** this piece of code
    is there, i.e. its **purpose**.

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

### What are "docstrings" and how can they be useful?

Here is function `fahrenheit_to_celsius` which converts temperature in
Fahrenheit to Celsius.

The first set of examples uses **regular comments**:

```python
# This function converts a temperature in Fahrenheit to Celsius.
def fahrenheit_to_celsius(temp_f: float) -> float:
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

The second set uses **docstrings or similar concepts**. Please compare the two
(above and below):

```py
def fahrenheit_to_celsius(temp_f: float) -> float:
    """
    Converts a temperature in Fahrenheit to Celsius.

    Parameters
    ----------
    temp_f : float
        The temperature in Fahrenheit.

    Returns
    -------
    float
        The temperature in Celsius.
    """

    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

Docstrings can do a bit more than just comments:  

- Tools can generate help text automatically from the docstrings.  

- Tools can generate documentation pages automatically from code.  

It is common to write docstrings for functions, classes, and modules.

Good docstrings describe:  

- What the function does.  

- What goes in (including the type of the input variables). 

- What goes out (including the return type).  

**Naming is documentation**:
Giving explicit, descriptive names to your code segments (functions, classes,
variables) already provides very useful and important documentation. In
practice you will find that for simple functions it is unnecessary to add a
docstring when the function name and variable names already give enough
information.

### User/API documentation
* What if a README file is not enough?
* How do I easily create user documentation?

### Tools
You can use the following tools to generate user or API documentation:

#### Sphinx (documentation generator)
- creates nicely-formatted HTML pages out of .md or .rst files
- programming language independent

#### Github pages (deploy your documentation)
- set up inside your GitHub repository
- automatically deploys your Sphinx-generated documentation

::: instructor
You can show the example documentation deployed on GitHub pages here: https://esciencecenter-digital-skills.github.io/good-practices-documentation-example/

Then, you can show that this content comes from simple markdown files, like: https://github.com/esciencecenter-digital-skills/good-practices-documentation-example/blob/main/doc/another-feature.md?plain=1

In addition, you can explain that with a few settings you can automatically generate documentation from docstrings. You can give https://nanopub.readthedocs.io/en/latest/reference/client.html as an example.

:::


:::::::::::::::::::::::::::::::::::::::: keypoints

- Good README files provide a good landing place for anyone that is new to your project

::::::::::::::::::::::::::::::::::::::::::::::::::
