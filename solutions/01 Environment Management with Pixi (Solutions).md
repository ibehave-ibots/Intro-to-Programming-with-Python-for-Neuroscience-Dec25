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

**Solution**:

```python
mkdir /tmp/my_project  # create tmp/my_project/
cd /tmp/my_project  # move to tmp/my_project
```

```
/tmp/my_project

```


**Exercise**: Run `pixi init` to initialize a new workspace in the current directory and open the `pixi.toml` file in VSCode.

**Solution**:

```python
pixi init
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Created /tmp/my_project/pixi.toml
</pre>


**Exercise**: Use `pixi add` to add Python to the environment.

**Solution**:

```python
pixi add python
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">python</span> <span style="font-weight: lighter">&gt;=3.14.2,&lt;3.15</span>
</pre>


**Exercise**: Use `pixi shell` to activate the environment and run `python --version` to print the version of the current python installation.

**NOTE**: Typing only `python` opens a Python shell. You can exit by typing `exit()`.

**Solution**:

```python
pixi shell
python --version
```

```
Python 3.14.2

```


**Exercise**: Use `pixi remove` to remove Python from the environment.

**Solution**:

```python
pixi remove python
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Removed <span style="font-weight: bold">python</span>
</pre>


**Exercise**: Add `python==3.12` to the environment

**Solution**:

```python
pixi add python==3.12
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">python==3.12</span>
</pre>


**Exercise**: Use `pixi shell` to activate the environment and run `python --version` to print the version of the current python installation.

**Solution**:

```python
pixi shell
python --version
```

```
Python 3.12.0

```


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

**Solution**:

```python
pixi add numpy matplotlib
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">numpy</span> <span style="font-weight: lighter">&gt;=2.3.5,&lt;3</span>
<span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">matplotlib</span> <span style="font-weight: lighter">&gt;=3.10.8,&lt;4</span>
</pre>


**Exercise**: Use `pixi list` to verify the packages were installed.

**Solution**:

```python
pixi list
```

<pre class="ansi-output"><span style="font-weight: bold">Package</span>                    <span style="font-weight: bold">Version</span>       <span style="font-weight: bold">Build</span>                 <span style="font-weight: bold">Size</span>        <span style="font-weight: bold">Kind</span>   <span style="font-weight: bold">Source</span>
_libgcc_mutex              0.1           conda_forge           2.5 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
_openmp_mutex              4.5           2_gnu                 23.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
alsa-lib                   1.2.14        hb9d3cd8_0            553.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
brotli                     1.2.0         hed03a55_1            19.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
brotli-bin                 1.2.0         hb03c661_1            20.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
bzip2                      1.0.8         hda65f42_8            254.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ca-certificates            2025.11.12    hbd8a1cb_0            148.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cairo                      1.18.4        h3394656_0            955.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
contourpy                  1.3.3         py312hd9148b4_3       288.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cycler                     0.12.1        pyhcf101f3_2          14.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cyrus-sasl                 2.1.28        hd9c7081_0            204.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
dbus                       1.16.2        h24cb091_1            437.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
double-conversion          3.3.1         h5888daf_0            67.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-dejavu-sans-mono  2.37          hab24e00_0            388.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-inconsolata       3.000         h77eed37_0            94.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-source-code-pro   2.038         h77eed37_0            684.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-ubuntu            0.83          h77eed37_3            1.5 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fontconfig                 2.15.0        h7e30c49_1            259.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonts-conda-ecosystem      1             0                     3.6 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonts-conda-forge          1             hc364b38_1            4 KiB       <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonttools                  4.61.1        py312h8a5da7c_0       2.8 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
freetype                   2.14.1        ha770c72_0            169.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
graphite2                  1.3.14        hecca717_2            97.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
harfbuzz                   12.2.0        h15599e2_0            2.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
icu                        75.1          he02047a_0            11.6 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
keyutils                   1.6.3         hb9d3cd8_0            130.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
kiwisolver                 1.4.9         py312h0a2e395_2       75.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
krb5                       1.21.3        h659f571_0            1.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
lcms2                      2.17          h717163a_0            242.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ld_impl_linux-64           2.45          default_hbd61a6d_104  708.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
lerc                       4.0.0         h0aef613_1            258 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libblas                    3.11.0        4_h4a7cf45_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlicommon            1.2.0         hb03c661_1            78.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlidec               1.2.0         hb03c661_1            33.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlienc               1.2.0         hb03c661_1            291.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libcblas                   3.11.0        4_h0358290_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libclang-cpp21.1           21.1.7        default_h99862b1_1    20.1 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libclang13                 21.1.7        default_h746c552_1    11.8 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libcups                    2.3.3         hb8b1518_5            4.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libdeflate                 1.25          h17f619e_0            71.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libdrm                     2.4.125       hb03c661_1            303.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libedit                    3.1.20250104  pl5321h7949ede_0      131.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libegl                     1.7.0         ha4b6fd6_2            43.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libexpat                   2.7.3         hecca717_0            74.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libffi                     3.5.2         h9ec8514_0            56.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libfreetype                2.14.1        ha770c72_0            7.5 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libfreetype6               2.14.1        h73754d4_0            377.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgcc                     15.2.0        he0feb66_16           1018.4 KiB  <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgcc-ng                  15.2.0        h69a702a_16           26.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgfortran                15.2.0        h69a702a_16           26.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgfortran5               15.2.0        h68bc16d_16           2.4 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgl                      1.7.0         ha4b6fd6_2            131.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglib                    2.86.2        h32235b2_0            3.8 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglvnd                   1.7.0         ha4b6fd6_2            129.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglx                     1.7.0         ha4b6fd6_2            73.7 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgomp                    15.2.0        he0feb66_16           589.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libiconv                   1.18          h3b78370_2            771.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libjpeg-turbo              3.1.2         hb03c661_0            618.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblapack                  3.11.0        4_h47877c9_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libllvm21                  21.1.7        hf7376ad_0            42.3 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblzma                    5.8.1         hb9d3cd8_2            110.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblzma-devel              5.8.1         hb9d3cd8_2            429.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libnsl                     2.0.1         hb9d3cd8_1            32.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libntlm                    1.8           hb9d3cd8_0            32.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libopenblas                0.3.30        pthreads_h94d23a6_4   5.7 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libopengl                  1.7.0         ha4b6fd6_2            49.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpciaccess               0.18          hb9d3cd8_0            27.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpng                     1.6.53        h421ea60_0            310.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpq                      18.1          h5c52fec_2            2.6 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libsqlite                  3.51.1        h0c1763c_0            917 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libstdcxx                  15.2.0        h934c35e_16           5.6 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libstdcxx-ng               15.2.0        hdf11a46_16           26.7 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libtiff                    4.7.1         h9d88235_1            425.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libuuid                    2.41.2        h5347b49_1            39.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libvulkan-loader           1.4.328.1     h5279c79_0            193 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libwebp-base               1.6.0         hd42ef1d_0            419 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxcb                     1.17.0        h8a09558_0            386.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxcrypt                  4.4.36        hd590300_1            98 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxkbcommon               1.13.1        hca5e8e5_0            818.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxml2                    2.15.1        h26afc86_0            44.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxml2-16                 2.15.1        ha9997c6_0            543.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxslt                    1.1.43        h711ed8c_1            239.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libzlib                    1.3.1         hb9d3cd8_2            59.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">matplotlib</span>                 3.10.8        py312h7900ff3_0       17 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
matplotlib-base            3.10.8        py312he3d6523_0       8.1 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
munkres                    1.1.4         pyhd8ed1ab_1          15.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ncurses                    6.5           h2d0b736_3            870.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">numpy</span>                      2.3.5         py312h33ff503_0       8.4 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openjpeg                   2.5.4         h55fea9a_0            347.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openldap                   2.6.10        he970967_0            762 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openssl                    3.6.0         h26f9b46_0            3 MiB       <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
packaging                  25.0          pyh29332c3_1          61 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pcre2                      10.46         h1321c63_0            1.2 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pillow                     12.0.0        py312h50c33e8_2       1004.5 KiB  <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pixman                     0.46.4        h54a6638_1            440.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pthread-stubs              0.4           hb9d3cd8_1002         8.1 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pyparsing                  3.2.5         pyhcf101f3_0          101.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pyside6                    6.9.3         py312h9da60e5_1       9.7 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">python</span>                     3.12.0        hab00c5b_0_cpython    30.6 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
python-dateutil            2.9.0.post0   pyhe01879c_2          227.8 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
python_abi                 3.12          8_cp312               6.8 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
qhull                      2020.2        h434a139_5            540 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
qt6-main                   6.9.3         h5c1c036_1            52.2 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
readline                   8.2           h8c095d6_2            275.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
six                        1.17.0        pyhe01879c_1          18 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tk                         8.6.13        noxft_ha0e22de_103    3.1 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tornado                    6.5.3         py312h4c3975b_0       831 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tzdata                     2025b         h8577fbf_1            116.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
unicodedata2               17.0.0        py312h4c3975b_1       398.8 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
wayland                    1.24.0        hd6090a7_1            322 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util                   0.4.1         h4f16b4b_2            20.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-cursor            0.1.6         hb03c661_0            20.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-image             0.4.0         hb711507_2            24 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-keysyms           0.4.1         hb711507_0            14 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-renderutil        0.3.10        hb711507_0            16.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-wm                0.4.2         hb711507_0            50.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xkeyboard-config           2.46          hb03c661_0            387.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libice                1.1.2         hb9d3cd8_0            57.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libsm                 1.2.6         he73a12e_0            26.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libx11                1.8.12        h4f16b4b_0            816.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxau                1.0.12        hb03c661_1            15 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxcomposite         0.4.6         hb9d3cd8_2            13.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxcursor            1.2.3         hb9d3cd8_0            31.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxdamage            1.1.6         hb9d3cd8_0            12.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxdmcp              1.1.5         hb03c661_1            20.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxext               1.3.6         hb9d3cd8_0            48.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxfixes             6.0.2         hb03c661_0            19.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxi                 1.8.2         hb9d3cd8_0            46.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxrandr             1.5.4         hb9d3cd8_0            28.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxrender            0.9.12        hb9d3cd8_0            32.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxtst               1.2.5         hb9d3cd8_3            32 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxxf86vm            1.1.6         hb9d3cd8_0            17.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz                         5.8.1         hbcc6ac9_2            23.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz-gpl-tools               5.8.1         hbcc6ac9_2            33.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz-tools                   5.8.1         hb9d3cd8_2            94.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
zlib-ng                    2.3.2         h54a6638_0            131.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
zstd                       1.5.7         hb78ec9c_6            587.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
</pre>


**Exercise**: Try installing the package `mtrfpy` from Conda-Forge. What does the error message say?

**Solution**:

```python
pixi add mtrfpy
```

<pre class="ansi-output">Error:   <span style="color: #aa0000">×</span> failed to solve the conda requirements of '<span style="color: #E850A8">default</span>' '<span style="color: #aa5500">linux-64</span>'
<span style="color: #aa0000">  ╰─▶ </span>Cannot solve the request because of: No candidates were found for mtrfpy
<span style="color: #aa0000">      </span>*.
<span style="color: #aa0000">      </span>

</pre>


**Exercise**: Install the `mtrf` package from `--pypi`.

**Solution**:

```python
pixi add --pypi mtrf
```

<pre class="ansi-output"><span style="color: #00aa00">✔ </span>Added <span style="font-weight: bold">mtrf</span> <span style="font-weight: lighter">&gt;=2.1.2, &lt;3</span>
Added these as <span style="font-weight: bold">pypi-dependencies</span>.
</pre>


**Exercise**: Open the `pixi.toml` file in VSCode and observe how the Conda-Forge and PyPI dependencies are listed separately. 

**NOTE**: The `pixi.toml` file also contains other (user specific) information like `author` and `platforms`.

**Solution**:

```
Content of pixi.toml: 

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

```


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

**Solution**:

```python
mkdir /tmp/reproduce
cp pixi.toml /tmp/reproduce
cp pixi.lock /tmp/reproduce
```


**Exercise**: Move to the new `reproduce/` directory and run `pixi install` to reproduce the environment there.

**Solution**:

```python
cd /tmp/reproduce
pixi install
```

<pre class="ansi-output"><span style="color: #aa5500"> WARN</span> Using local manifest /tmp/my_project/pixi.toml rather than /home/olebi/projects/new-learning-platform/pixi.toml from environment variable `PIXI_PROJECT_MANIFEST`
<span style="color: #00aa00">✔ </span>The <span style="color: #E850A8">default</span> environment has been installed.
</pre>


**Exercise**: Run `pixi list` and check the installed version of `numpy` and ensure it matches the version in the original environment

**Solution**:

```python
pixi list
```

<pre class="ansi-output"><span style="color: #aa5500"> WARN</span> Using local manifest /tmp/my_project/pixi.toml rather than /home/olebi/projects/new-learning-platform/pixi.toml from environment variable `PIXI_PROJECT_MANIFEST`
<span style="font-weight: bold">Package</span>                    <span style="font-weight: bold">Version</span>       <span style="font-weight: bold">Build</span>                 <span style="font-weight: bold">Size</span>        <span style="font-weight: bold">Kind</span>   <span style="font-weight: bold">Source</span>
_libgcc_mutex              0.1           conda_forge           2.5 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
_openmp_mutex              4.5           2_gnu                 23.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
alsa-lib                   1.2.14        hb9d3cd8_0            553.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
array_api_compat           1.12.0                              189.1 KiB   <span style="color: #0000aa">pypi</span>   array_api_compat-1.12.0-py3-none-any.whl
brotli                     1.2.0         hed03a55_1            19.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
brotli-bin                 1.2.0         hb03c661_1            20.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
bzip2                      1.0.8         hda65f42_8            254.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ca-certificates            2025.11.12    hbd8a1cb_0            148.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cairo                      1.18.4        h3394656_0            955.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
contourpy                  1.3.3         py312hd9148b4_3       288.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cycler                     0.12.1        pyhcf101f3_2          14.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
cyrus-sasl                 2.1.28        hd9c7081_0            204.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
dbus                       1.16.2        h24cb091_1            437.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
double-conversion          3.3.1         h5888daf_0            67.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-dejavu-sans-mono  2.37          hab24e00_0            388.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-inconsolata       3.000         h77eed37_0            94.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-source-code-pro   2.038         h77eed37_0            684.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
font-ttf-ubuntu            0.83          h77eed37_3            1.5 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fontconfig                 2.15.0        h7e30c49_1            259.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonts-conda-ecosystem      1             0                     3.6 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonts-conda-forge          1             hc364b38_1            4 KiB       <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
fonttools                  4.61.1        py312h8a5da7c_0       2.8 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
freetype                   2.14.1        ha770c72_0            169.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
graphite2                  1.3.14        hecca717_2            97.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
harfbuzz                   12.2.0        h15599e2_0            2.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
icu                        75.1          he02047a_0            11.6 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
keyutils                   1.6.3         hb9d3cd8_0            130.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
kiwisolver                 1.4.9         py312h0a2e395_2       75.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
krb5                       1.21.3        h659f571_0            1.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
lcms2                      2.17          h717163a_0            242.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ld_impl_linux-64           2.45          default_hbd61a6d_104  708.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
lerc                       4.0.0         h0aef613_1            258 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libblas                    3.11.0        4_h4a7cf45_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlicommon            1.2.0         hb03c661_1            78.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlidec               1.2.0         hb03c661_1            33.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libbrotlienc               1.2.0         hb03c661_1            291.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libcblas                   3.11.0        4_h0358290_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libclang-cpp21.1           21.1.7        default_h99862b1_1    20.1 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libclang13                 21.1.7        default_h746c552_1    11.8 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libcups                    2.3.3         hb8b1518_5            4.3 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libdeflate                 1.25          h17f619e_0            71.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libdrm                     2.4.125       hb03c661_1            303.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libedit                    3.1.20250104  pl5321h7949ede_0      131.5 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libegl                     1.7.0         ha4b6fd6_2            43.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libexpat                   2.7.3         hecca717_0            74.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libffi                     3.5.2         h9ec8514_0            56.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libfreetype                2.14.1        ha770c72_0            7.5 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libfreetype6               2.14.1        h73754d4_0            377.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgcc                     15.2.0        he0feb66_16           1018.4 KiB  <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgcc-ng                  15.2.0        h69a702a_16           26.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgfortran                15.2.0        h69a702a_16           26.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgfortran5               15.2.0        h68bc16d_16           2.4 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgl                      1.7.0         ha4b6fd6_2            131.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglib                    2.86.2        h32235b2_0            3.8 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglvnd                   1.7.0         ha4b6fd6_2            129.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libglx                     1.7.0         ha4b6fd6_2            73.7 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libgomp                    15.2.0        he0feb66_16           589.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libiconv                   1.18          h3b78370_2            771.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libjpeg-turbo              3.1.2         hb03c661_0            618.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblapack                  3.11.0        4_h47877c9_openblas   18.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libllvm21                  21.1.7        hf7376ad_0            42.3 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblzma                    5.8.1         hb9d3cd8_2            110.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
liblzma-devel              5.8.1         hb9d3cd8_2            429.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libnsl                     2.0.1         hb9d3cd8_1            32.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libntlm                    1.8           hb9d3cd8_0            32.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libopenblas                0.3.30        pthreads_h94d23a6_4   5.7 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libopengl                  1.7.0         ha4b6fd6_2            49.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpciaccess               0.18          hb9d3cd8_0            27.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpng                     1.6.53        h421ea60_0            310.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libpq                      18.1          h5c52fec_2            2.6 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libsqlite                  3.51.1        h0c1763c_0            917 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libstdcxx                  15.2.0        h934c35e_16           5.6 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libstdcxx-ng               15.2.0        hdf11a46_16           26.7 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libtiff                    4.7.1         h9d88235_1            425.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libuuid                    2.41.2        h5347b49_1            39.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libvulkan-loader           1.4.328.1     h5279c79_0            193 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libwebp-base               1.6.0         hd42ef1d_0            419 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxcb                     1.17.0        h8a09558_0            386.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxcrypt                  4.4.36        hd590300_1            98 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxkbcommon               1.13.1        hca5e8e5_0            818.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxml2                    2.15.1        h26afc86_0            44.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxml2-16                 2.15.1        ha9997c6_0            543.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libxslt                    1.1.43        h711ed8c_1            239.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
libzlib                    1.3.1         hb9d3cd8_2            59.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">matplotlib</span>                 3.10.8        py312h7900ff3_0       17 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
matplotlib-base            3.10.8        py312he3d6523_0       8.1 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #0000aa"></span><span style="font-weight: bold; color: #0000aa">mtrf</span>                       2.1.2                               68.1 KiB    <span style="color: #0000aa">pypi</span>   mtrf-2.1.2-py3-none-any.whl
munkres                    1.1.4         pyhd8ed1ab_1          15.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
ncurses                    6.5           h2d0b736_3            870.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">numpy</span>                      2.3.5         py312h33ff503_0       8.4 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openjpeg                   2.5.4         h55fea9a_0            347.1 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openldap                   2.6.10        he970967_0            762 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
openssl                    3.6.0         h26f9b46_0            3 MiB       <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
packaging                  25.0          pyh29332c3_1          61 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pcre2                      10.46         h1321c63_0            1.2 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pillow                     12.0.0        py312h50c33e8_2       1004.5 KiB  <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pixman                     0.46.4        h54a6638_1            440.4 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pthread-stubs              0.4           hb9d3cd8_1002         8.1 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pyparsing                  3.2.5         pyhcf101f3_0          101.6 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
pyside6                    6.9.3         py312h9da60e5_1       9.7 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
<span style="color: #00aa00"></span><span style="font-weight: bold; color: #00aa00">python</span>                     3.12.0        hab00c5b_0_cpython    30.6 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
python-dateutil            2.9.0.post0   pyhe01879c_2          227.8 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
python_abi                 3.12          8_cp312               6.8 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
qhull                      2020.2        h434a139_5            540 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
qt6-main                   6.9.3         h5c1c036_1            52.2 MiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
readline                   8.2           h8c095d6_2            275.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
six                        1.17.0        pyhe01879c_1          18 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tk                         8.6.13        noxft_ha0e22de_103    3.1 MiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tornado                    6.5.3         py312h4c3975b_0       831 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
tzdata                     2025b         h8577fbf_1            116.2 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
unicodedata2               17.0.0        py312h4c3975b_1       398.8 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
wayland                    1.24.0        hd6090a7_1            322 KiB     <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util                   0.4.1         h4f16b4b_2            20.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-cursor            0.1.6         hb03c661_0            20.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-image             0.4.0         hb711507_2            24 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-keysyms           0.4.1         hb711507_0            14 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-renderutil        0.3.10        hb711507_0            16.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xcb-util-wm                0.4.2         hb711507_0            50.5 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xkeyboard-config           2.46          hb03c661_0            387.7 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libice                1.1.2         hb9d3cd8_0            57.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libsm                 1.2.6         he73a12e_0            26.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libx11                1.8.12        h4f16b4b_0            816.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxau                1.0.12        hb03c661_1            15 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxcomposite         0.4.6         hb9d3cd8_2            13.3 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxcursor            1.2.3         hb9d3cd8_0            31.8 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxdamage            1.1.6         hb9d3cd8_0            12.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxdmcp              1.1.5         hb03c661_1            20.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxext               1.3.6         hb9d3cd8_0            48.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxfixes             6.0.2         hb03c661_0            19.6 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxi                 1.8.2         hb9d3cd8_0            46.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxrandr             1.5.4         hb9d3cd8_0            28.9 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxrender            0.9.12        hb9d3cd8_0            32.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxtst               1.2.5         hb9d3cd8_3            32 KiB      <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xorg-libxxf86vm            1.1.6         hb9d3cd8_0            17.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz                         5.8.1         hbcc6ac9_2            23.4 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz-gpl-tools               5.8.1         hbcc6ac9_2            33.1 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
xz-tools                   5.8.1         hb9d3cd8_2            94.2 KiB    <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
zlib-ng                    2.3.2         h54a6638_0            131.9 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
zstd                       1.5.7         hb78ec9c_6            587.3 KiB   <span style="color: #00aa00">conda</span>  https://conda.anaconda.org/conda-forge/
</pre>


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

**Solution**:

```python
pixi shell
python hello.py
```

```
Hello World!

```


**Exercise**: Now use `pixi run` to execute the Python script without having to activate the environment first.

**Solution**:

```python
pixi run python hello.py
```

```
Hello World!

```


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