---
layout: reference
---

## Additional Syntax

In this course we have deliberately chosen to use a single approach to creating and activating Conda environments and
installing packages within them, following the pattern of _Create > Activate > Install_. This was done to avoid
confusing and overwhelming participants with the multitude of options because there are other methods/syntax for
combining these steps that achieve the same end result.

### Creating and Installing packages in one command

It is possible to create a Conda environment _and_ install specific Python packages within it (from Conda repositories
at least, not using `pip` to install packages from  [PyPI](https://pypi.org)) in a single step. This negates the need to
specify a version of Python to install (i.e. `python=3.10`) as it will be pulled in as a dependency of the Python
package.

For example to create the `basic-scipy-env` created whilst working through Chapter 2 you could use the following.

~~~
$ conda create --name basic-scipy-env numba scikit-learn=1.2.0 ipython matplotlib=3.7 scipy=1.9.3
$ conda activate basic-scipy-env
~~~
{: .language-bash}

### Namespaces

An alternative method of specifying the channel from which you wish to install a specific package from is know as
"Namespaces" where the package is preceded by the channel from which you wish to install it from and separated by two
semi-colons.

For example to install the `polars` package from the `conda-forge` channel within the `my-final-project` environment as
is done Chapter 3 you could use the following.

~~~
$ conda create --name my-final-project python=3.10
$ conda activate my-final-project
$ conda install jupyterlab matplotlib conda-forge::polars
~~~
{: .language-bash}

This can even be combined with the above example of creating and installing packages at the same time to give the
following.

~~~
$ conda create --name my-final-project python=3.10 jupyterlab matplotlib conda-forge::polars
$ conda activate my-final-project
~~~
{: .language-bash}

## Glossary



{% include links.md %}
