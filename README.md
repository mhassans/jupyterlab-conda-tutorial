# jupyterlab-conda-tutorial
Repository for creating a conda environment to use with JupyterLab

### Clone this repository to use example notebook

    git clone git@github:albertdow/jupyterlab-conda-tutorial.git

## Setting up JupyterLab (only needs to be done once - read through before deciding what to do!)
### For concise version use "Quick install instructions" (see below)
### If you already have a python3 conda environment you can skip this part

First log into lx02 or lx03 (this is what I use).

I recommend to install miniconda which is a python package manager
and useful for many things, especially when you don't have root access.

Follow instructions here 
(https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)
or do what I propose next:

Basically you need to get the relevant installer and install it.
I recommend doing this in `/vols/build/` as there is more space:

    wget https://repo.anaconda.com/miniconda/Miniconda2-latest-Linux-x86_64.sh

and then run it with

    bash Miniconda2-latest-Linux-x86_64.sh

and follow instructions.

Then you can create a new virtual environment with 

    conda create -n myenv python=3  

Then you can activate the environment with

    conda activate myenv

and add all desired packages with

    pip install <package1> <package2> etc..

eg. 

    pip install jupyterlab

A useful list of things to have is `numpy scipy pandas scikit-learn uproot matplotlib`

To not activate conda by default every time you log into lx02 do:

    conda config --set auto_activate_base false

If you want to simply copy the environment I use (which should have quite a lot of the 
things you would need + ROOT 6.18 installed as well, i.e. you can work outside
of CMSSW completely if you like):

    conda env create -n myenv_py3 --file environment.yml python=3

This command may take a while.

### Quick install instructions for conda with JupyterLab:

Run the following commands in `/vols/build/` in `lx02`:

    wget https://repo.anaconda.com/miniconda/Miniconda2-latest-Linux-x86_64.sh

    bash Miniconda2-latest-Linux-x86_64.sh # and follow instructions.

    conda config --set auto_activate_base false

Now go to cloned albertdow/jupyterlab-conda-tutorial directory and run 

    conda env create --n myenv_py3 --file environment.yml python=3

### If you already have a python3 conda environment:

Just activate that environment and pip install jupyterlab.

## Setting up JupyerLab session (do this every time):

### Activate conda environment:

    conda activate myenv_py3

### Setting up a tunnel:

Set up an ssh tunnel using your local machine/laptop by logging into
lx02 the way you normally do adding `-Y -N -L localhost:<port>:localhost:<port>`

So for example I do (if you have your lx02 set-up in you ssh config):

    ssh -Y -N -L localhost:1234:localhost:1234 lx02

or otherwise

    ssh -Y -N -L localhost:1234:localhost:1234 <username>@lx02.hep.ph.ic.ac.uk

__Note: this port needs to be unique, so choose a random four-digit number.
Also keep the terminal you did this in open as this will keep the tunnel active.__

### Setting up a JupyterLab server in lx02

Then set up a jupyter lab session in lx02 using same port as for tunnelling:

    jupyter lab --no-browser --port=1234

Follow instructions by copying the printed link into your browser and you should be ready to go.

Now open the provided `example_for_ICtaus.ipynb` notebook from inside JupyterLab; you 
should be able to find it in the current directory if that is where you created the
server. For running the example plot, also set-up CMS plotting style (see below).

(By the way, I recommend using tmux to keep the JupyterLab server active even if ssh connection drops or you log out)

### CMS plotting style (used in the example notebook)
To have proper CMS-style plots get the CMS style from

    export MPLCONFIGDIR=./mpl_configdir/

