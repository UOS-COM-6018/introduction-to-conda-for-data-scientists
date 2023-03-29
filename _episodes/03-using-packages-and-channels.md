---
title: "Using Conda Channels and PyPI (`pip`)"
teaching: 20
exercises: 10
questions:
- "What are Conda channels?"
- "Why should I be explicit about which channels my research project uses?"
- "What should I do if a Python package isn't available via a Conda channel?"
objectives:
- "Install a package from a specific channel."
keypoints:
- "A package is a compressed archive file containing system-level libraries, Python or other modules, executable programs and other components, and associated metadata."
- "A Conda channel is a URL to a directory containing a Conda package(s)."
- "Conda and Pip can be used together effectively."
---

## What are Conda channels?

Conda packages are downloaded from
remote channels, which are URLs to directories containing conda packages. The `conda` command
searches a standard set of channels, referred to as `defaults`. The `defaults` channels include:

*   `main`: The majority of all new Anaconda, Inc. package builds are hosted here. Included in
    `defaults` as the top priority channel.
*   `r`: Microsoft R Open conda packages and [Anaconda, Inc.'s R conda packages](https://anaconda.org/r/repo).

Unless otherwise specified, packages installed using `conda` will be downloaded from the `defaults`
channels.

> ## The `conda-forge` channel
>
> In addition to the `defaults` channels that are managed by Anaconda Inc., there is another channel that also has

> a special status. The [Conda-Forge](https://github.com/conda-forge) project "_is a community led collection of
> recipes, build infrastructure and distributions for the conda package manager._"
>
> There are a few reasons that you may wish to use the `conda-forge` channel instead of the
> `defaults` channel maintained by Anaconda:
>
> 1. Packages on `conda-forge` may be more up-to-date than those on the `defaults` channel.
> 2. There are packages on the `conda-forge` channel that aren't available from `defaults`.
> 3. You may wish to use a dependency such as `openblas` (from `conda-forge`) instead of `mkl`
> (from `defaults`).
{: .callout}

## My package isn't available in the `defaults` channels! What should I do?

You may find that packages (or often more recent versions of packages!) that you need to
install for your project are not available on the `defaults` channels.  In this case you could try the
following channels.

1.  `conda-forge`: the `conda-forge` channel contains a large number of community curated Conda
    packages. Typically the most recent versions of packages that are generally available via the
    `defaults` channel are available on `conda-forge` first.
2. `bioconda`: the `bioconda` channel also contains a large number of Bioinformatics curated conda packages.
    `bioconda` channel is meant to be used with `conda-forge`, you should not worried about using the two channels
    when installing your prefered packages.

For example, [Kaggle](https://www.kaggle.com/) publishes a Python 3 API that can be used to interact with Kaggle
datasets, kernels and competition submissions. You can search for the package on the `defaults` channels but you will
not find it!

~~~
$ conda search kaggle
Loading channels: done
No match found for: kaggle. Search: *kaggle*

PackagesNotFoundError: The following packages are not available from current channels:

  - kaggle

Current channels:

  - https://repo.anaconda.com/pkgs/main/osx-64
  - https://repo.anaconda.com/pkgs/main/noarch
  - https://repo.anaconda.com/pkgs/free/osx-64
  - https://repo.anaconda.com/pkgs/free/noarch
  - https://repo.anaconda.com/pkgs/r/osx-64
  - https://repo.anaconda.com/pkgs/r/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page.
~~~
{: .language-bash}

Let's check whether the package exists on at least `conda-forge` channel. 
Note that the [official installation instructions](https://github.com/Kaggle/kaggle-api) 
suggest a different way to install.

~~~
$ conda search --channel conda-forge kaggle
Loading channels: done
# Name                       Version           Build  Channel
kaggle                         1.5.3          py27_1  conda-forge
kaggle                         1.5.3          py36_1  conda-forge
kaggle                         1.5.3          py37_1  conda-forge
kaggle                         1.5.4          py27_0  conda-forge
kaggle                         1.5.4          py36_0  conda-forge
kaggle                         1.5.4          py37_0  conda-forge
.
.
.
kaggle                        1.5.12  py38h578d9bd_1  conda-forge
kaggle                        1.5.12  py38h578d9bd_2  conda-forge
kaggle                        1.5.12  py39hf3d152e_0  conda-forge
kaggle                        1.5.12  py39hf3d152e_1  conda-forge
kaggle                        1.5.12  py39hf3d152e_2  conda-forge
kaggle                        1.5.12    pyhd8ed1ab_4  conda-forge
~~~
{: .language-bash}

Or you can also check online at [https://anaconda.org/conda-forge/kaggle](https://anaconda.org/conda-forge/kaggle).

Once we know that the `kaggle` package is available via `conda-forge` we can go ahead and install
it.

~~~
$ conda install --channel conda-forge kaggle=1.5.12  --name machine-learning-env
~~~
{: .language-bash}

> ## Channel priority
>
> You may specify multiple channels for installing packages by passing the `--channel` argument
> multiple times.
>
> ~~~
> $ conda install scipy=1.10.0 --channel conda-forge --channel bioconda
> ~~~
> {: .language-bash}
>
> Channel priority decreases from left to right - the first argument has higher priority than the
> second. For reference, [bioconda](https://bioconda.github.io/) is a channel for the conda package manager specializing
> in bioinformatics software. For those interested in learning more about the Bioconda project, checkout the project's
> [GitHub](https://bioconda.github.io/) page.
>
> Please note that in our example, adding `bioconda` channel is irrelevant because `scipy` is no longer available on
> `bioconda` channel.
{: .callout}

> ## Specifying channels when installing packages
>
> `polars` is an alternative to `pandas` written in the Rust programming language, so it runs faster.
>
> Create a Python 3.10 environment called
> `fast-analysis-project` with the `polars` package. Also include the most recent versions of `jupyterlab`
> (so you have a nice UI) and `matplotlib` (so you can make plots) in your environment .
>
> > ## Solution
> >
> > Optionally, check what versions of `polars` are available so you can install a specific version. 
> > Then create a new Conda environment (`conda create`) with the versions of Python,
> > and packages required.
> >
> > ~~~
> > $ conda create --name fast-analysis-project --channel conda-forge python=3.10 jupyterlab polars matplotlib
> > ~~~
> > {: .language-bash}
> >
> > Hint: the `--channel` argument can also be shortened to `-c`, for more
> > abbreviations, see also the
> > [Conda command reference](https://docs.conda.io/projects/conda/en/latest/commands.html) .
> {: .solution}
{: .challenge}

## Using `pip` and Conda

You can use the default Python package
manager [`pip`](https://pip.pypa.io/en/stable/) to install packages from [Python Package Index
(PyPI)](https://pypi.org/). However, there are a few [potential
issues](https://www.anaconda.com/blog/using-pip-in-a-conda-environment) that you should be aware of when using `pip` to
install Python packages when using Conda.

First, `pip` is sometimes installed by default on operating systems where it is used to manage any Python packages
needed by your OS. **You do not want to use `/usr/bin/pip` to install Python packages when using Conda
environments.**

~~~
(base) $ conda deactivate
$ which python
/usr/bin/python
$ which pip # sometimes installed as pip3
/usr/bin/pip
~~~
{: .language-bash}

> ## Windows users...
>
> You can type `where.exe` in **PowerShell** and it does the same thing as `which` in **bash**.
{: .callout}

Second, `pip` is also included in the Miniconda installer where it is used to install and manage OS specific Python
packages required to setup your `base` Conda environment. **You do not want to use this `~/miniconda3/bin/pip` to
install Python packages when using Conda environments.**

~~~
$ conda activate
(base) $ which python
~/miniconda3/bin/python
$ which pip
~/miniconda3/bin/pip
~~~
{: .language-bash}

> ## Why should I avoid installing packages into the `base` Conda environment?
>
> If your `base` Conda environment becomes cluttered with a mix of `pip` and Conda installed
> packages it may no longer function. Creating separate Conda environments allows you to
> delete and recreate environments readily so you dont have to worry about risking your core
> Conda functionality when mixing packages installed with Conda and Pip.
{: .callout}

If you find yourself needing to install a Python package that is only available via PyPI, then you should use the copy of
`pip`, which is installed automatically when you create a Conda environment with Python, to install the desired package
from PyPI. Using the `pip` installed in your Conda environment to install Python packages not available via Conda
channels will help you avoid difficult to debug issues that frequently arise when using Python packages installed via a
`pip` that was not installed inside you Conda environment.

> ## Conda (+Pip)
>
> Pitfalls of using Conda and `pip` together can be avoided by 
> always ensuring your **desired environment is active** before installing anything using `pip`.
{: .callout}

> ## Installing packages into Conda environments using `pip`
>
> [Combo](https://github.com/yzhao062/combo) is a comprehensive Python toolbox for combining
> machine learning models and scores. Model combination can be considered as a subtask of
> [ensemble learning](https://en.wikipedia.org/wiki/Ensemble_learning), and has been widely used
> in real-world tasks and data science competitions like [Kaggle](https://www.kaggle.com/).
>
> Activate the `machine-learning-env` you created in a previous challenge and use `pip` to install
> `combo`.
>
> > ## Solution
> >
> > The following commands will activate the `machine-learning-env` and install `combo`.
> >
> > ~~~
> > $ conda activate machine-learning-env
> > $ pip install combo==0.1.*
> > ~~~
> > {: .language-bash}
> >
> > For more details on using `pip` see the [official documentation](https://pip.pypa.io/en/stable/).
> {: .solution}
{: .challenge}

{% include links.md %}
