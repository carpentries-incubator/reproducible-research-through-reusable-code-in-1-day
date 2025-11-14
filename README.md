# Reproducible research through reusable code

This is the lesson material for the workshop 'Reproducible research through reusable code in 1 day.'
This workshop teaches you the skills to make your code reusable by others. 
In one day you will share your coding project on GitHub and work on 
the minimal requirements needed for others to run your code.
At the end of the day we will do a short reusability check of each other's repository.

## Teaching this lesson?
This material is open-source and freely available. 
Are you planning on using our material in your teaching? 
We would love to help you prepare to teach the lesson and receive feedback on how it could be further improved, based on your experience in the workshop.

You can notify us that you plan to teach this lesson by creating an issue in this repository. Also, it would be great if you can update [this overview of all workshops taught with this lesson material](workshops.md). 
This helps us show the impact of developing open-source lessons to our funders.

## Target audience
This workshop is aimed at researchers who want to make their code reusable. 
You are able to write basic code in a programming language like R or Python. 
This can be a few simple lines of code or a larger piece of software.

Participants must bring their own coding project to the workshop. This can range from a few small scripts to an extensive piece of software. 

If you are already familiar with using version control and GitHub, 
documenting dependencies of your project, basic software documentation, 
and basic coding conventions, and the basics of modular coding than this course is probably to introductory for you.


## Setup the Workshop Website locally

To build this lesson locally, you should follow the [setup instructions for the
workbench](https://carpentries.github.io/sandpaper-docs/#overview). In short,
make sure you have R, Git, and Pandoc installed, open R and use the following
commands to install/update the packages needed for the infrastructure:

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

## Rendering the website locally

See the [Carpentries Workbench usage instructions](https://carpentries.github.io/workbench/#usage) on how to render the website locally.

## Maintainer(s)

Current maintainers of this lesson are
* Sven van der Burg (svenvanderburg@gmail.com)
* Eduard Klapwijk (et.klapwijk@gmail.com)
