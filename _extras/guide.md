---
title: "Instructor Notes"
---

# Modules, packages, libraries

* Module: a collection of functions and variables, as in a script
* Package: a collection of modules with an __init__.py file (can be empty), as in a directory with scripts
* Library: a collection of packages with related functionality

Library/Package are often used interchangeably.

# Environment management systems for Python

Conda is not the only way; Python for example has many more ways of working with environments:
* [virtualenv](https://virtualenv.pypa.io/en/latest/)
* [pipenv](https://pipenv.pypa.io/en/latest/)
* [venv](https://docs.python.org/3/library/venv.html)
* [pyenv](https://github.com/pyenv/pyenv)
* [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/)

# Package management systems for Python
Also here, Conda is not the only way; Python for example has many more ways of working with packages:
* [pip](https://pip.pypa.io/en/stable/)
* [Poetry](https://python-poetry.org/)
* [PDM](https://pdm.fming.dev/latest/)
* ...

# Conda on HPC systems

Many HPC systems make either Miniconda or Anaconda (or both!) available to users via 
[Environment Modules](http://modules.sourceforge.net/). In this case a user will need to load the 
relevant module instead of installing Conda.

~~~
$ module load miniconda
~~~
{: .language-bash}

> ## Avoid running the `conda init` command
> 
> Using the `conda init` command is not advisable on HPC systems that use Environment Modules 
> to make Miniconda or Anaconda available to users.  The reason is that running the `conda init` 
> command makes changes to a user's `~/.bashrc` file. If the user subsequently forgets to reverse 
> these changes using `conda init --reverse`, then `conda` will still be available even after 
> unloading or purging the `miniconda` module.  This opens the distinct possibility of a user 
> accidently leaving his/her shell environment in an unexpected state.
{: .callout}

# Virtual Machines

A **virtual machine** is a representation of a real, physical computer created using software. A single
physical computer can host multiple virtual machines and each can be configured completely differently
including having different operating systems - a physical computer running Windows can host Linux
virtual machines, and *vice versa*.

## Alternative syntax for installing packages from specific channels
There exists an alternative syntax for installing conda packages from specific channels that
more explicitly links the channel being used to install a particular package.
~~~
$ conda install conda-forge::tensorflow --name computer-vision-project
~~~
{: .language-bash}
Repeat the previous exercise using this alternative syntax to install `python`, `jupyterlab`, and `matplotlib` from the
`conda-forge` channel and `pytorch` and `torchvision` from the `pytorch` channel.

{% include links.md %}
