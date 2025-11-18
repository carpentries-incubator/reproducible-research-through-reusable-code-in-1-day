---
title: "Further improvements to your project"
teaching: 5
exercises: 45
---

:::::::::::::::::::::::::::::::::::::: questions 

- What other improvements can I make to make my project more reproducible?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Add a license to your project
- Add `howfairis` badge to your README file
- Add information about how to cite your project
- Link your project to Zenodo
- Add data to your project

::::::::::::::::::::::::::::::::::::::::::::::::

In this part we will add some further improvements to making your project more reproducible.

Try to prioritize what you think will be most beneficial to your project.

::: challenge
## Add a license to your project
Pick a license and add it to the repository.
Use https://choosealicense.com/ to find a license for your project. 
Or if you do not know, you can use [Apache License 2.0](https://choosealicense.com/licenses/apache-2.0/){target="_blank"}, a common permissive open-source license.
To get some more background information about licenses, the [licensing chapter from the Turing Way](https://book.the-turing-way.org/reproducible-research/licensing/)
is a good starting point. 

:::

::: challenge
## Add `fairsoftwarechecklist.net` badge to your README file
Add the [![FAIR checklist badge](https://fairsoftwarechecklist.net/badge.svg)](https://fairsoftwarechecklist.net/v0.2?f=00&a=00000&i=00000&r=000){target="_blank"} 
badge to your README file. Do the self-assessment for FAIR research software on [fairsoftwarechecklist.net](https://fairsoftwarechecklist.net/){target="_blank"}
and link to your answers using the badge.

Alternatively, you can add the [![FAIR software badge](https://img.shields.io/badge/fair--software.eu-%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F-green)](https://fair-software.eu/){target="_blank"} 
badge to your README. Follow [the instructions on the howfairis GitHub repo](https://github.com/fair-software/howfairis){target="_blank"} to run an automated check
on your code repository.

How FAIR is your project and what do you need to do to improve it?
Read more about FAIR software at [https://fair-software.eu/](https://fair-software.eu/){target="_blank"}

:::

::: challenge
## Add information about how to cite your project.

Use [cff-initializer](https://citation-file-format.github.io/cff-initializer-javascript/#/){target="_blank"} to create a CITATION.cff 
file for your project.

:::

::: challenge
## Link your project to Zenodo.

1. Create an account at [Zenodo](https://zenodo.org/){target="_blank"}
2. [Link your GitHub repository to Zenodo](https://zenodo.org/account/settings/github/){target="_blank"}. Follow the instructions on the page.

By publishing your repository on Zenodo, it will receive a persistent identifier. This will help to avoid link rot, and make your project more FAIR.

:::

::: challenge
## Add data to your project.

Make sure you are allowed to publish the data (most importantly, it should be de-identified 
in the case of human participants). 

Publish the data in a data repository and include the link to your data set in your GitHub 
repository. Data repositories offer organized and structured storage and access of data, 
ensuring that data sets abide by the [FAIR principles](https://www.go-fair.org/fair-principles/){target="_blank"}
, allowing data are findable, accessible, interoperable, and reusable (FAIR) as much as 
possible. 

Alternatively, you can include a data file in your GitHub repository. In case you are unable 
to share the data, include dummy data in the project.

Make sure all data files are saved in a 
[sustainable file format](https://dans.knaw.nl/en/file-formats/){target="_blank"} such as .csv, 
and that the files and variables are [properly named](https://doi.org/10.5281/zenodo.7551576){target="_blank"}
and clearly described.


:::


:::::::::::::::::::::::::::::::::::::::: keypoints

- There are various ways to improve the reproducibility of your project.

::::::::::::::::::::::::::::::::::::::::::::::::::
