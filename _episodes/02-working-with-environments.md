---
title: "Working with Environments"
teaching: 60
exercises: 15
questions:
- "What is a Conda environment?"
- "How do I create (delete) an environment?"
- "How do I activate (deactivate) an environment?"
- "How do I install packages into existing environments using Conda?"
- "How do I find out what packages have been installed in an environment?"
- "How do I find out what environments that exist on my machine?"
- "How do I delete an environment that I no longer need?"
objectives:
- "Understand how Conda environments can improve your research workflow."
- "Create a new environment."
- "Activate (deactivate) a particular environment."
- "Install packages into existing environments using Conda."
- "List all of the existing environments on your machine."
- "List all of the installed packages within a particular environment."
- "Delete an entire environment."
keypoints:
- "A Conda environment is a directory that contains a specific collection of Conda packages that you have installed."
- "You create (remove) a new environment using the `conda create` (`conda remove`) commands."
- "You activate (deactivate) an environment using the `conda activate` (`conda deactivate`) commands."
- "You install packages into environments `conda install`."
- "Use the `conda env list` command to list existing environments and their respective locations."
- "Use the `conda list` command to list all of the packages installed in an environment."
- "Use the `conda [command] --help` to get information on how to use conda or a specific `command`."
---

> ## Workspace for Conda environments
> If you haven't done it yet, create a new `conda-environments-for-effective-and-reproducible-research` directory on your Desktop in
> order to maintain a consistent workspace for all the material covered in this course. The Conda environments are not
> stored there but other files will be.
>
> On Mac OSX and Linux running following commands in the
> Terminal will create the required directory on the Desktop.
>
> ~~~
> $ cd ~/Desktop
> $ mkdir conda-environments-for-effective-and-reproducible-research
> $ cd conda-environments-for-effective-and-reproducible-research
> ~~~
> {: .language-bash}
>
>
> For Windows users you may need to reverse the direction of the slash and run
> the commands from the command prompt.
>
> ~~~
> > cd ~\Desktop
> > mkdir conda-environments-for-effective-and-reproducible-research
> > cd conda-environments-for-effective-and-reproducible-research
> ~~~
>
> Alternatively, you can always "right-click" and "create new folder" on your Desktop. All the
> commands that are run during the workshop should be run in a terminal within the
> `conda-environments-for-effective-and-reproducible-research` directory.
>
{: .callout}

## What is a Conda environment?

A [Conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html)
is a directory that contains a specific collection of Conda packages that you have installed. For
example, you may be working on a research project that requires [NumPy
1.24.1](https://github.com/numpy/numpy/releases/tag/v1.24.1) and its dependencies, while another environment associated
with an finished project has [NumPy 1.12.1](https://github.com/numpy/numpy/releases/tag/v1.12.1) (perhaps because
version 1.12 was the most current version of NumPy at the time the project finished). If you change one environment,
your other environments are not affected. You can easily activate or deactivate environments, which is how you switch
between them.

> ## Avoid installing packages into your `base` Conda environment
>
> Conda has a default environment called `base` that includes a Python installation and some core system libraries and
> dependencies of Conda. It is a "best practice" to avoid installing additional packages into your `base` software
> environment as this can cause dependency complications further down the line.  Additional packages needed for a new
> project should always be installed into a newly created Conda environment.
{: .callout}


> ## Conda has a help system
>
> Conda has a built in help system that can be called from the command line if you are unsure of the commands/syntax to
> use.
>
> ~~~
> $ conda --help
> ~~~
>
> If you want to read the help on a specific sub-command/action then use `conda <action> --help` for example to read the
> help on `install` use.
>
> ~~~
> $ conda install --help
> ~~~
{: .callout}
## Creating environments

To create a new environment for Python development using `conda` you can use the `conda create` command.

~~~
$ conda create --name basic-scipy-env
~~~
{: .language-bash}

For a list of all commands, take a look at [Conda general commands](https://docs.conda.io/projects/conda/en/latest/commands.html).

It is a good idea to give your environment a meaningful name in order to help yourself remember
the purpose of the environment. While naming things can be difficult, `$PROJECT_NAME-env` is a
good convention to follow. Sometimes including the version of Python you created the environment
with is useful too.

The command above created a new Conda environment called `basic-scipy-env` and installed a recent
version of Python (3.10 if you downloaded the most recent install script). You can however specify a specific version of
Python for `conda` to install when creating the environment by adding a version number e.g. to `python=3.8`.

~~~
$ conda create --name python38-env python=3.8
~~~
{: .language-bash}


## Activating an existing environment

Activating environments is essential to making the software in environments work well (or sometimes at all!). Activation
of an environment does two things.

1. Adds entries to `$PATH` for the environment.
2. Runs any activation scripts that the environment may contain.

Step 2 is particularly important as activation scripts are how packages can set arbitrary environment variables that may
be necessary for their operation. You activate the `basic-scipy-env` environment by name using the `activate` command.

~~~
$ conda activate basic-scipy-env
~~~
{: .language-bash}

You can see that an environment has been activated because the shell prompt will now include the name of the active
environment.

~~~
(basic-scipy-env) $
~~~

> ## Creating and activating a new environment
>
> Create a new environment called "machine-learning-39-env" with Python 3.9 explicitly specified and  activate it
>
> > ## Solution
> >
> > In order to create a new environment you use the `conda create` command
> >
> > ~~~
> > $ conda create --name machine-learning-39-env python=3.9
> > $ conda activate machine-learning-39-env
> > ~~~
> > {: .language-bash}
> >
> {: .solution}
{: .challenge}



## Deactivate the current environment

To deactivate the currently active environment use the Conda `deactivate` command as follows.

~~~
(basic-scipy-env) $ conda deactivate
~~~
{: .language-bash}

You can see that an environment has been deactivated because the shell prompt will no longer
include the name of the previously active environment, but will return to `base`.

~~~
(base) $
~~~

> ## Returning to the `base` environment
>
> To return to the `base` Conda environment, it's better to call `conda activate` with no
> environment specified, rather than to use `deactivate`. If you run `conda deactivate` from your
> `base` environment, you may lose the ability to run `conda` commands at all. **Don't worry if
> you encounter this undesirable state! Just start a new shell or `source ~/.bashrc` if you are on
> a Linux or OSX system.**
{: .callout}

> ## Activate an existing environment by name
>
> Activate the `machine-learning-39-env` environment created in the previous challenge by name.
>
> > ## Solution
> >
> > In order to activate an existing environment by name you use the `conda activate` command as
> > follows.
> >
> > ~~~
> > $ conda activate machine-learning-39-env
> > ~~~
> > {: .language-bash}
> {: .solution}
{: .challenge}

> ## Deactivate the active environment
>
> Deactivate the `machine-learning-39-env` environment that you activated in the previous challenge.
>
> > ## Solution
> >
> > In order to deactivate the active environment you could use the `conda deactivate` command.
> >
> > ~~~
> > (active-environment-name) $ conda deactivate
> > ~~~
> > {: .language-bash}
> >
> > Or you could switch back to the `base` conda environment this way.
> > ~~~
> > (active-environment-name) $ conda activate
> > ~~~
> > {: .language-bash}
> {: .solution}
{: .challenge}

## Installing a package into an existing environment

You can install a package into an existing environment using the `conda install` command. This
command accepts a list of package specifications (i.e., `numpy=1.18`) and installs a set of
packages consistent with those specifications *and* compatible with the underlying environment. If
full compatibility cannot be assured, an error is reported and the environment is *not* changed.

By default the `conda install` command will install packages into the current, active environment. The following would
activate the `basic-scipy-env` we created above and install [`Numba`](https://numba.pydata.org/), an open source JIT
(Just In Time) compiler that translates a subset of Python and `numpy` code into fast machine code, into the active
environment.

~~~
$ conda activate basic-scipy-env
$ conda install numba
~~~
{: .language-bash}

If version numbers are not explicitly provided, Conda will attempt to install the newest versions of any requested
packages. To accomplish this, Conda may need to update some packages that are already installed or install additional
packages. It is sometimes a good idea to explicitly provide version numbers when installing packages with the `conda
install` command. For example, the following would install a particular version of Scikit-Learn into the current,
active environment.

~~~
$ conda install scikit-learn=1.2
~~~
{: .language-bash}

> ## You can specify a version number for each package you wish to install
>
> In order to make your results reproducible and to make it easier for research colleagues to recreate your Conda
> environments on their machines it is sometimes a good practice to explicitly specify the version number for each
> package that you install into an environment.
>
> Many packages use [semantic versioning](https://semver.org/)  where there are three version numbers separated by
> decimal points e.g. 2.11.3. In this scheme the numbers have this meaning:
> _major_version_._minor_version_._patch_version_. Changes to  _patch_version_ are for backwards compatible bug fixes,
> so we often only specify the first two numbers.
>
> If you are not sure exactly which version of a package you want to use, then you can use search to see what versions
> are available using the `conda search` command.
>
> ~~~
> $ conda search <PACKAGE_NAME>
> ~~~
>
> For example, if you wanted to see which versions of [Scikit-learn](https://scikit-learn.org/stable/),
> a popular Python library for machine learning, are available, you would run the following.
>
> ~~~
> $ conda search scikit-learn
> ~~~
>
> As always you can run `conda search --help` to learn about available options.
{: .callout}


When `conda` installs a package into an environment it also installs any required dependencies. For example, even though
`numpy` was not listed as a package to install when `numba` was installed `conda` will still install `numpy` into the environment because it is a required dependency of `numba`.

You can install multiple packages by listing the packages that you wish to install, optionally including the version you
wish to use.

~~~
$ conda activate basic-scipy-env
$ conda install ipython matplotlib=3.7 scipy=1.9
~~~
{: .language-bash}

> ## What actually happens when I install packages?
>
> During the installation process, files are extracted into the specified environment (defaulting to
> the current environment if none is specified). Installing the files of a Conda package into an
> environment can be thought of as changing the directory to an environment, and then downloading
> and extracting the package and its dependencies. Conda does the hard work of figuring out what
> dependencies are needed and making sure that they will all work together.
{: .callout}

Running the following command in the `basic-scipy-env` will fail as the requested `scipy` and `numpy` versions are
incompatible with Python 3.10 the environment was created with (`numpy=1.9.3` is quite an old version).

~~~
$ conda install scipy=1.9.3 numpy=1.9.3
~~~
{: .language-bash}

> ## Discussion
>
> What are some of the _potential_ benefits of specifying versions of each package, what
> are some of the _potential_ drawbacks.
>
> > ## Solution
> > Specifying versions exactly helps make it more likely that the exact results of an analysis
> > will be reproducible e.g. at a later time or on a different computer. However, not all versions
> > of a package will be compatible with all versions of another, so specifying exact versions can
> > make it harder to add or change packages in the future, limiting reusability e.g. with different
> > data.
> >
> {: .solution}
{: .challenge}


> ## Freezing installed packages
>
> To prevent existing packages from being updated when using the `conda install` command, you can
> use the `--freeze-installed` option. This may force Conda to install older versions of the
> requested packages in order to maintain compatibility with previously installed packages. Using
> the `--freeze-installed` option does not prevent additional dependency packages from being
> installed.
{: .callout}

> ## Installing a package into a specific environment
>
> [`dask`](https://dask.org/)
> provides advanced parallelism for data science workflows enabling performance at scale for the
> core Python data science tools such as `numpy`, `pandas`, and `scikit-learn`. Have a read through the
> [official documentation](https://docs.conda.io/projects/conda/en/latest/commands/install.html)
> for the `conda install` command and see if you can figure out how to install `dask` into the
> `machine-learning-39-env` that you created in the previous challenge.
>
> > ## Solution
> >
> > You can activate the `machine-learning-39-env` environment, search for available versions of `dask` and then use the
> > `conda install` command as follows.
> > ~~~
> > $ conda activate machine-learning-39-env
> > $ conda search dask
> > $ conda install dask=2022.7.0
> > ~~~
> > {: .language-bash}
> >
> {: .solution}
{: .challenge}

> ## Listing existing environments
>
> Now that you have created a number of Conda environments on your local machine you have probably
> forgotten the names of all of the environments and exactly where they live. Fortunately, there is
> a `conda` command to list all of your existing environments together with their locations.
>
> ~~~
> $ conda env list
> # conda environments:
> #
> base                  *  /home/neil/miniconda3
> basic-scipy-env          /home/neil/miniconda3/envs/basic-scipy-env
> machine-learning-39-env  /home/neil/miniconda3/envs/machine-learning-39-env
> python310-env            /home/neil/miniconda3/envs/python310-env
> scikit-learn-env         /home/neil/miniconda3/envs/scikit-learn-env
> scikit-learn-kaggle-env  /home/neil/miniconda3/envs/scikit-learn-kaggle-env
> ~~~
> {: .language-bash}
>
> ## Where do Conda environments live?
>
> Another method of finding out where your Conda environment live if you're not sure is to use `conda --info` which
> provides the location of the active directory (`active env location :`) and the location environments are stored
> (`envs directories : `) along with additional information.
>
> ~~~
> conda info
>
>     active environment : base
>    active env location : /home/neil/miniconda3
>            shell level : 1
>         user config file : /home/neil/.condarc
>   populated config files : /home/neil/miniconda3/.condarc
>                          /home/neil/.condarc
>          conda version : 23.1.0
>    conda-build version : not installed
>         python version : 3.10.8.final.0
>       virtual packages : __archspec=1=x86_64
>                          __glibc=2.37=0
>                          __linux=6.2.6=0
>                          __unix=0=0
>       base environment : /home/neil/miniconda3  (writable)
>      conda av data dir : /home/neil/miniconda3/etc/conda
>  conda av metadata url : None
>           channel URLs : https://repo.anaconda.com/pkgs/main/linux-64
>                          https://repo.anaconda.com/pkgs/main/noarch
>                          https://repo.anaconda.com/pkgs/r/linux-64
>                          https://repo.anaconda.com/pkgs/r/noarch
>          package cache : /home/neil/miniconda3/pkgs
>                          /home/neil/.conda/pkgs
>       envs directories : /home/neil/miniconda3/envs
>                          /home/neil/.conda/envs
>               platform : linux-64
>             user-agent : conda/23.1.0 requests/2.28.1 CPython/3.10.8 Linux/6.2.6-arch1-1 arch/ glibc/2.37
>                UID:GID : 1000:1000
>              netrc file : None
>             offline mode : False
> ~~~
> {: .bash}
>
>
{: .callout}


## Listing the contents of an environment

In addition to forgetting names and locations of Conda environments, at some point you will probably forget exactly what
has been installed in a particular Conda environment. Again, there is a `conda` command for listing the contents on an
environment. To list the contents of the `basic-scipy-env` that you created above, run the following command.

~~~
$ conda list --name basic-scipy-env
~~~
{: .language-bash}

> ## Listing the contents of a particular environment.
>
> List the packages installed in the `machine-learning-env` environment that you created in a previous challenge.
>
> > ## Solution
> >
> > You can list the packages and their versions installed in `machine-learning-env` using the `conda list` command as
> > follows.
> > ~~~
> > $ conda list --name machine-learning-env
> > ~~~
> > {: .language-bash}
> >
> > To list the packages and their versions installed in the active environment leave off
> > the `--name` option.
> > ~~~
> > $ conda list
> > ~~~
> > {: .language-bash}
> >
> {: .solution}
{: .challenge}

## Deleting entire environments

Occasionally, you will want to delete an entire environment. Perhaps you were experimenting with `conda` commands and
you created an environment you have no intention of using; perhaps you no longer need an existing environment and just
want to get rid of cruft on your machine. Whatever the reason, the command to delete an environment is the following.

~~~
$ conda remove --name first-conda-env --all
~~~
{: .language-bash}

> ## Delete an entire environment
>
> Delete the entire "basic-scipy-env" environment.
>
> > ## Solution
> >
> > In order to delete an entire environment you use the `conda remove` command as follows.
> >
> > ~~~
> > $ conda remove --name basic-scipy-env --all --yes
> > ~~~
> > {: .language-bash}
> >
> > This command will remove all packages from the named environment before removing the
> > environment itself. The use of the `--yes` flag short-circuits the confirmation prompt (and
> > should be used with caution).
> >
> {: .solution}
{: .challenge}

{% include links.md %}
