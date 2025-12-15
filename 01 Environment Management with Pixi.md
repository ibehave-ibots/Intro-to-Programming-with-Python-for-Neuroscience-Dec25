Most software we are using comes with a list of dependencies which, in turn, have their own dependencies. This means that any given piece of software requires a specific environment of other packages to function properly.
The larger the tree of dependencies, the more likely it is that two pieces of software have a version conflict because they require different versions of the same dependency.
This can be prevented by using virtual environments.
Virtual environments are self-contained boxes that are used only within a specific narrow scope.
By creating a dedicated virtual environment for every project we can isolate the software and avoid conflicts.
We can also improve the reproducibility of our research because the virtual environment can be shared together with the code and data.

In this notebook, you are going to learn how to use Pixi - a fast and modern tool for managing virtual environments.
Pixi allows us to set up new projects and install packages very quickly and with few steps.
What's more, Pixi keeps track of our environment as we add new dependencies.
It creates a manifest called `pixi.toml` which contains a list of the dependencies we specified.
It also creates a file called `pixi.lock` which contains a comprehensive description of the virtual environment (i.e. the whole tree of dependencies).
These files allow us to exactly reproduce the computational environment.

**NOTE**: The exercises in this notebook assume that you have installed [Pixi](https://pixi.sh/latest/#installation) and [Visual Studio Code](https://code.visualstudio.com/download). If you haven't, just click on the link and follow the instructions for your operating system on the website. To test if Pixi was installed correctly, open a terminal (in VSCode select View>Terminal from the menu bar or press Ctrl+\`) and type `pixi --version`. If you are getting an error that the command was not found, try restarting VSCode.


## Creating and Managing Environments

### Background

To create a new Pixi project, open the terminal and move to the directory where you want to initialize the workspace.
On Windows, you can also use the file explorer to go to the target directory and Right Click > Open in Terminal.
Once you are in the directory, run `pixi init` which will create the manifest `pixi.toml` that contains all dependencies you specified.
Once you start installing dependencies, Pixi will create a `.pixi/` directory where the installed software is stored as well as a `pixi.lock` file that contains an exact description of the current computational environment.
To activate the environment, type `pixi shell`.
Once the environment is activated, you'll have access to all of the software installed with Pixi.

### Exercises

In the following exercises, you are going to create a new Pixi workspace, install Python and activate the virtual environment. Here are the commands you need to know.

| Code                    | Description                                                 |
|-------------------------|-------------------------------------------------------------|
| `cd my_dir/`            | Change the directory to `my_dir/`                           |
| `cd .. `                | Change the directory to the parent of the current directory |
| `mkdir new_dir/ `       | Create the directory `new_dir/`                             |
| `pixi init`             | Initialize a new Pixi project with a `pixi.toml`            |
| `pixi add python`       | add python to your environment                              |
| `pixi add python==3.13` | add Python version 3.13 to your environment                 |
| `pixi remove python`    | Remove python from your environment                         |
| `pixi shell`            | Activate the virtual environment                            |


**Example**: Create a new empty directory and move to that directory.

```python
mkdir /tmp/new_project # create /tmp/new_project/
cd /tmp/new_project # move to /tmp/new_project/
```

```
/tmp/new_project

```

**Exercise**: Create another new directory and move there. You can use your file explorer or the `mkdir` and `cd` commands as shown in the example above.


**Exercise**: Run `pixi init` to initialize a new workspace in the current directory and open the `pixi.toml` file in VSCode.


**Exercise**: Use `pixi add` to add Python to the environment.


**Exercise**: Use `pixi shell` to activate the environment and run `python --version` to print the version of the current python installation.

**NOTE**: Typing only `python` opens a Python shell. You can exit by typing `exit()`.


**Exercise**: Use `pixi remove` to remove Python from the environment.


**Exercise**: Add `python==3.12` to the environment


**Exercise**: Use `pixi shell` to activate the environment and run `python --version` to print the version of the current python installation.


## Installing Python Packages with Pixi

### Background

There are two prominent places for publishing Python packages: Conda-Forge and the Python Package Index (PyPI). A nice feature of Pixi is that it can resolve dependencies across both repositories (i.e. it can make sure there is no version conflict between Conda and PyPI packages).

Per default, Pixi installs packages from Conda but we can tell it to install PyPI packages by adding the `--pypi` flag. Conda-forge tests distribution and integration more systematically and is able bundle packages with non-Python dependencies (e.g. C-libraries). However, many libraries (especially smaller ones) are only available on PyPI. Thus, it is recommended that you install packages from Conda-Forge and only use PyPI if a given package is not available there.

### Exercises

In the following exercises you are going to install Python packages from Conda-Forge and PyPI. Here are the commands you need to know:

| Code                         | Description                                           |
|------------------------------|-------------------------------------------------------|
| `pixi add numpy`             | Install `numpy` from Conda-Forge                      |
| `pixi add --pypi numpy`      | Install package from PyPI                             |
| `pixi remove numpy`          | Remove `numpy` from the environment                   |
| `pixi add matplotlib pandas` | Install multiple packages (`matplotlib` and `pandas`) |
| `pixi shell`                 | Activate the virtual environment                      |
| `pixi list`                  | View all currently installed packages                 |

**Exercise**: Install the packages `numpy` and `matplotlib` from Conda-Forge.

**Exercise**: Use `pixi list` to verify the packages were installed.

**Exercise**: Try installing the package `mtrfpy` from Conda-Forge. What does the error message say?

**Exercise**: Install the `mtrf` package from `--pypi`.

**Exercise**: Open the `pixi.toml` file in VSCode and observe how the Conda-Forge and PyPI dependencies are listed separately. 

**NOTE**: The `pixi.toml` file also contains other (user specific) information like `author` and `platforms`.

## Sharing and Reproducing Environments

### Background

Pixi keeps track of all the dependencies we specify in our `pixi.toml` file.
At the same time, it is keeping track of all packages in the virtual environment (including the dependencies of our dependencies) in the `pixi.lock` file.

The lock file allows us to exactly reproduce the pixi environment in a different directory or even on a different machine by simply copying the `pixi.lock` file and running `pixi install`.

### Exercises

In the following exercises, you'll reproduce the current pixi environment from the `pixi.lock` file.
Here are the commands you need to know:

| Code                      | Description                                                 |
|---------------------------|-------------------------------------------------------------|
| `mkdir new_dir/ `         | Create the directory `new_dir/`                             |
| `cp file.txt new_dir/ `   | Copy `file.txt` to `new_dir/` (Linux/MacOS)                 |
| `copy file.txt new_dir/ ` | Copy `file.txt` to `new_dir/` (Windows)                     |
| `cd new_dir `             | Change the directory to `new_dir`                           |
| `cd .. `                  | Change the directory to the parent of the current directory |
| `pixi install`            | Install the environment from `pixi.lock`                    |


**Exercise**: Create a new directory called `reproduce/` and copy `pixi.toml` and `pixi.lock` to this location. You can either use your file explorer or the terminal commands `mkdir` and `cp`.

**Exercise**: Move to the new `reproduce/` directory and run `pixi install` to reproduce the environment there.

**Exercise**: Run `pixi list` and check the installed version of `numpy` and ensure it matches the version in the original environment

## Running Python Scripts with Pixi Environments

### Background 

So far, we used Pixi to install Python as well as some packages but we never ran any code. In this section we are going to run a very simple Python script that simply prints `"Hello World!"` and run it in the Pixi environment we created.

To do this we could use `pixi shell` to activate the environment (as we did before) and then run the environment. However, we can make things even simpler and use the `pixi run` command which combines activating the environment and running the script in a single step.

### Exercises

| Code                         | Description                                                        |
|------------------------------|--------------------------------------------------------------------|
| `pixi shell`                 | Activate the virtual environment                                   |
| `python analyse.py`          | Run the Python script `analyze.py`                                 |
| `pixi run python analyze.py` | Run the Python script `analyze.py` in the current Pixi environment |

**Exercise**: Copy the code in the cell below and save it to a file called `hello.py`.

```python
print("Hello World!")
```

**Exercise**: Use `pixi shell` to activate the virtual environment. Then, run `python hello.py` to run the Python script.

**NOTE**: If `hello.py` is not located in your current directory you must specify the full path, e.g. `my_directory/hello.py`.


**Exercise**: Now use `pixi run` to execute the Python script without having to activate the environment first.

## Demo: Managing Multiple Environments

One strength of Pixi is its ability to manage projects that require multiple environments.
This can be useful for research steps with multiple computation steps (e.g. preprocessing, statistics, visualization) that have different, incompatible dependencies.
Pixi has two different concepts that are relevant here: features and environments.
A feature is simply a set of packages with a specific name and an environment is a collection of features.

For this demo, lets create a little mock example. We'll use the packages `cowsay` and `pyfiglet` in two separate environments. While there is no actual dependency conflict between these packages it illustrates how we can isolate different parts of our code with dedicated environments.

First, we add the packages `cowsay` and `pyfiglet` and use the `-f` flag to assign each to a specific feature. Here, the features are called `cow` and `fig`. If you run the code you may get errors saying that these features do not belong to any environment - you can ignore these errors for now.

```python
!pixi add --pypi -q -f cow cowsay
!pixi add --pypi -q -f fig pyfiglet
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">cowsay</span>
Added these as <span style="font-weight: bold">pypi-dependencies</span>.
Added these only for feature: <span style="color: #00aaaa">cow</span>
<span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">pyfiglet</span>
Added these as <span style="font-weight: bold">pypi-dependencies</span>.
Added these only for feature: <span style="color: #00aaaa">fig</span>
</pre>

Let's look at the content of `pixi.toml`.
The dependencies listed in `[dependencies]` will be available for every environment while those listed under the `[feature]` headings will only be available in the environments that use these features.

```python
!cat pixi.toml
```

```
[workspace]
authors = ["obi <ole.bialas@posteo.de>"]
channels = ["conda-forge"]
name = "my_project"
platforms = ["linux-64"]
version = "0.1.0"

[tasks]

[dependencies]
python = "==3.12"
numpy = ">=2.3.5,<3"
matplotlib = ">=3.10.8,<4"

[pypi-dependencies]
mtrf = ">=2.1.2, <3"

[feature.cow.pypi-dependencies]
cowsay = "*"

[feature.fig.pypi-dependencies]
pyfiglet = "*"

```

To create the environments we create a new heading called `[environments]` that define each environment as a list of features:

```
[environments]
env1=["cow"]
env2=["fig"]
```

Here, the environments are called `env1` and `env2` and contain the features `"cow"` and `"fig"` respectively.
Each environment could also contain multiple features and the same feature can be used in multiple environments.

Now we can run `cowsay` in the environment `env1` and `pyfiglet` in the environment `env2`. We specify the environment for the run command using the `-e` flag.

```python
!pixi run -q -e env1 cowsay -t "Hello World"
```

```
  ___________
| Hello World |
  ===========
           \
            \
              ^__^
              (oo)\_______
              (__)\       )\/\
                  ||----w |
                  ||     ||

```

```python
!pixi run -q -e env2 pyfiglet "Hello World"
```

```
 _   _      _ _        __        __         _     _ 
| | | | ___| | | ___   \ \      / /__  _ __| | __| |
| |_| |/ _ \ | |/ _ \   \ \ /\ / / _ \| '__| |/ _` |
|  _  |  __/ | | (_) |   \ V  V / (_) | |  | | (_| |
|_| |_|\___|_|_|\___/     \_/\_/ \___/|_|  |_|\__,_|
                                                    


```