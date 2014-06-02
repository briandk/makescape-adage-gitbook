# The Tools We Use

We believe in reproducible research. We want our peers and colleagues to be able to inspect our methods, recreate our computations, and verify our results. To that end, **all the software tools we work with are freely available (zero cost) to anyone in the world**, with most of those tools also being open-source.

Here's what we think of as our [solution stack](http://en.wikipedia.org/wiki/Solution_stack) for data analysis.

### Version Control

- [Git](http://git-scm.com/)
- [Github.com](https://github.com/)
- The Github apps for [Mac](https://mac.github.com/) and [Windows](https://windows.github.com/)

To us, it's important that we preserve every historical stage of our data analysis, especially if we need to revert something we did. Git gives us a fast, industry-standard way to do that. We can version *everything*: code, images, even arbitrary binary files. And while some of us are command-line ninjas, we do most of our interaction with Git through the wonderful apps developed by the Github folks.

The most important advantage of using Git? We can throw our projects on Github and that gives us all sorts of advantages for collaboration: [pull requests](https://help.github.com/articles/using-pull-requests) for code review, discussion threads, and [issue trackers](https://github.com/blog/831-issues-2-0-the-next-generation). Heck, just [read the list of Github features](https://github.com/features) if you're not already convinced.


### Data Analysis in Python

- [Python](https://www.python.org/)
- [Pandas Data Analysis Library for Python](http://pandas.pydata.org/)
- [iPython Notebook](http://ipython.org/notebook.html)
- [Enthought Canopy Express](https://www.enthought.com/canopy-express/)

Python forms the core of the data analysis you'll see throughout this book. And, much of the code uses syntax from Pandas, a fantastic data analysis system built atop Python's excellent [Numpy](http://www.numpy.org/) (pronounced "Num-pie") and [Scipy](http://www.scipy.org/) packages.

But while Python is the language we speak, essentially all of this analysis was carried out in iPython Notebook. iPython Notebook is an amazing piece of software that lets code, plots, and documentation all live within the same dynamic document.

We use a turnkey version of Python called Enthough Canopy Express because it comes pre-loaded with everything we need: Numpy, Scipy, Pandas, and iPython. It's ready to go out of the box, and it's free.


### Data Analysis in R (not covered in this book)

- [The R Project for Statistical Computing](http://www.r-project.org/)
- [RStudio](http://www.rstudio.com/)

We don't always depart from Python, but when we do we use R. R is a powerful, open-source statistical programming language, and RStudio is a fantastic integrated development environment (IDE) for working in R. One of R's core strengths is its vast ecosystem of user-contributed packages. Odds are that if you want to do something special in R, there's a package for it. As of June 1, 2014 the R Package Archive has more than 5,000 packages available for use.


### Dissemination of Results

- [Github.com](https://github.com/)
- [iPython Notebook Viewer](http://nbviewer.ipython.org/) (for Python Analyses)
- [Markdown](http://en.wikipedia.org/wiki/Markdown) and [RMarkdown](http://www.rstudio.com/ide/docs/authoring/using_markdown)
- [Rpubs](https://rpubs.com/) (for R analyses)

Markdown is a simplified markup syntax originally developed by [John Gruber](http://daringfireball.net/projects/markdown/) and [Aaron Swartz](http://en.wikipedia.org/wiki/Aaron_Swartz). It's the backbone of all the text we write. (This entire book was written in Markdown!). We like it because it's a plaintext format that lets humans easily read and write rich text.

Also, you'll notice some repeat tools here, and there's a good reason for that. All of the above tools work together for sharing our work. The general workflow is:

1. Write a [literate document](http://en.wikipedia.org/wiki/Literate_programming) with code, plots, and narrative all in one
2. Version the document with git
3. Push the repository to Github, where it can be shared
4. Optionally, create a persistent link using a publication service

When we work in Python, we use iPython to create [literate documents](http://en.wikipedia.org/wiki/Literate_programming) with raw Python code, annotated with Markdown. If we version those notebooks with git, we can then easily push the code repository to Github. And, with the repository on Github we can point iPython Notebook Viewer to our file. Whenever our file updates, the iPython Notebook Viewer page automatically updates too, so our analysis can evolve over time.

We use a similar workflow for R, which has its own publication service for RMarkdown Documents called [Rpubs](https://rpubs.com/).
