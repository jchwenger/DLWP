# Deep Learning Installation Requirements

### Important Note

The easiest way to work with these notebooks is simply to open them in [Google Colab](https://colab.research.google.com/) (or another provider of online compute such as [Amazon SageMaker](https://aws.amazon.com/sagemaker/ai/studio/) or [Kaggle Notebooks](https://www.kaggle.com/code)), which has already everything installed. During the course, this is what is assumed. Google Colab comes with a nice integration with [Google Drive](https://drive.google.com/drive/), that allows you to save your progress and keep your files (`.ipynb`).

The way this works is:
1) Upload any `.ipynb` file (or the entire folder) to your Drive.
2) Right-click (Windows/Linux) / CTLR+click (MacOS) on the `.ipynb` file, -> Open with.
3) The first time you do this, do Connect more apps, search "Colab", Install. After that, you'll always be able to select "Google Collaboratory" in the list (in fact, once Colab is installed, you can just double click on any notebook file and it opens in Colab automatically).

The notes below are there for two use-cases:
- open and work on notebooks locally;
- people who own a machine with a GPU or for whatever reason want to engage more deeply with Python environments and `conda`.

What follows assumes a fresh installation, and the use of the terminal. However, if you already have Anaconda installed, you can always install `mamba` (faster `conda`) in any existing environment, and so continue working with Anaconda.

## 1 Installation

With Python, it is **essential to work with environments**, which work like isolated, separated spaces (if things break or get complicated, you can erase them and start over). Installing/uninstalling dependencies in your OS Python can lead to various kinds of software breaking down, it is highly not recommended.

Here are some [slides on Python Installation & environments](https://docs.google.com/presentation/d/1aTYSvpuYaE_dPIWwT_HEcYve7fsYpDtzix74d5-NvC4/edit?usp=sharing).

The recommended path to install Python for all platforms is through [Miniforge](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install) (as this includes `mamba`, see below).

On Windows, I recommend allowing Miniforge to be your primary Python provider and adding it to the PATH of all terminals (so you can access `mamba/conda` in them). (I also recommend installing [Git-Bash](https://gitforwindows.org/). Note that lower-level libraries (Tensorflow certainly) usually require Linux to run on GPU.)

Once this is installed, in a new terminal, install the course dependencies:

```bash
$ mamba env create -f environment.yml
```

If you need to update the environment using the YAML file, do this:

```bash
$ mamba env update -f environment.yml
```

Now you can activate the environment:

```bash
$ mamba activate dlwp
(dlwp) $ # the environment is active
(dlwp) $ jupyter lab # open Jupyter to read notebooks
```

To deactivate:

```bash
(dlwp) $ mamba deactivate
$ # the environment is no longer active
```

You can obviously add dependencies manually, but **always** check that your environment is active when you do so (the name should appear in parentheses before the terminal prompt, and the location of python/pip – use `which python` on UNIX systems; `where python` on Windows – should be inside the environment, e.g. `/Users/jcw/miniforge3/envs/dlwp/bin/python`).

### Anaconda/Miniconda/Miniforge: A History

For managing Python environment (and more), use mamba (faster replacement of conda)! Works on Linux/MacOS/Windows.

The very short history of all these names are:
- First came [Anaconda](https://www.anaconda.com/) – another big snake, like Python –, which is the full install (only recommended if you use it elsewhere or are only comfortable with GUI software);
- Then [Miniconda](https://docs.conda.io/en/latest/miniconda.html), the minimal install, CLI only;
- Then given the slowness of `conda` due to many different [channels](https://www.anaconda.com/docs/getting-started/concepts/what-is-a-channel) and dependencies conflict, one channel, [Conda Forge](https://conda-forge.org/), decided to create their own minimal and fast 'Anaconda' called [Miniforge](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install) (originally Mambaforge), using this channel as a priority, and developing their own reimplementation of `conda`, [`mamba`](https://mamba.readthedocs.io/en/latest/installation/mamba-installation.html) (smaller snake, faster since it's a C++ reimplementation of `conda`).

**NOTE: when using `conda/mamba`, it is *strongly* recommended never to use the `base` environment, the one coming out of the box with `conda`, and that `conda` needs to update itself (installing things in this environment runs the risk of slowing down any update you want to make to `conda` itself). Just leave it as is and always work in an environment _you_ created.**

### Note: Creating Environments Manually

We already have an environment ready, let's create a new python 3.x environment (if you're using Anaconda, then you can always do `conda install mamba` and use `mamba` after that):

```bash
$ mamba create -n dlwp python=3.12
```

Note: "dlwp" ("Deep Learning With Python") is just a name, you can pick whatever you like.

```bash
$ mamba activate dlwp # after that your prompt will show the env
(dlwp) $ mamba install keras tensorflow
# you can use `mamba` (or `pip`) to install dependencies
# (use `mamba` for installation, much faster than `conda`)
```

Check packages:

```bash
$ conda activate dlwp
(dlwp) $ conda list # the entire list
(dlwp) $ conda list | grep -i keras # search for one package
```

See [this cheatsheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf) for more.

## 2 Running Jupyter

### 2.1 From Anaconda (recommended)

Launch Anaconda, **select your environment** and launch Jupyter. You can then navigate your file system to find the folder with your notebooks.

### 2.2 Jupyter, from the command line

Navigate to the folder where you keep your project files.

```bash
$ conda activate dlwp
(dlwp) $ jupyter lab
```

Press ctrl-c twice in the terminal to close Jupyter.
