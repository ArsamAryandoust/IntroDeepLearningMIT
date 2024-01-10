# Introduction to Deep Learning MIT 2024

This repository contains environment setup instructions and software lab solutions
for the Independent Activity Period (IAP) course 6.S191 
[Introduction to Deep Learning](http://introtodeeplearning.com/) taught at MIT 
during January 2024. 

If you are affiliated with MIT and want to use the 
[Satori compute cluster](https://satori-portal.mit.edu/) for accomplishing the 
[Software Labs of the course](https://github.com/aamini/introtodeeplearning), 
follow the instructions we provide here to correctly set up a custom Jupyter 
kernel for this purpose.

## Login

Login to the satori cluster with your personal account using your <mit_username>.
You can use one of the following two commands:

```
ssh <mit_username>@satori-login-001.mit.edu
ssh <mit_username>@satori-login-002.mit.edu
```


## Deactive conda

Upon login, you will automatically be in a default conda environment (base). 
Before you set up a custom environment and kernel, deactivate conda with the 
following command:

```
conda deactivate
```


## Set up conda directories

Set up the conda environment directories using your own <mit_username>. Do this
under `/nobackup/users/<mit_username>` as you have more storage available here
than in your home folder on Satori:

```
CKNAME=IntroDeepLearningMIT
CKUSER=arsam
CKROOT=projects/condas

mkdir -p /nobackup/users/${CKUSER}/${CKROOT}/${CKNAME}
```


## Install Miniconda

Create your own Miniconda installation for the custom kernel:

```
cd /nobackup/users/${CKUSER}/${CKROOT}/${CKNAME}
wget https://repo.continuum.io/miniconda/Miniconda2-4.7.12.1-Linux-ppc64le.sh
chmod +x Miniconda2-4.7.12.1-Linux-ppc64le.sh
./Miniconda2-4.7.12.1-Linux-ppc64le.sh -b -p `pwd`/miniconda3
. miniconda3/etc/profile.d/conda.sh
export PATH="`pwd`/miniconda3/bin:$PATH"
```


## Create base environment

Create, activate and update your base conda environment. For this project, 
`tensorflow-gpu` is a good choice as it sets up all the GPU drivers and configurations
we need:

```
conda create -y --name ${CKNAME} tensorflow-gpu
conda activate ${CKNAME}
conda update -n base -c defaults conda
```

## Install custom packages

Now we can customize our conda environment by installing all the packages that
we need for our software labs. For the 2024 course, the following packages have
to be installed. Note, that jupyterlab is required for running our notebooks
from the browser. Alternatively, you can also install jupyter, which provides 
the simpler jupyter notebook sessions only. You can use both pip and conda to
customize your environment. Depending on the package, one may work better than
the other. Commands:

```
conda install conda-forge::opencv #it's normal to take a couple minutes
pip install --user matplotlib
pip install --user mitdeeplearning
pip install --user jupyterlab
```

## Launch notebooks

We now have a fully customized conda environment with all required packages and
drivers installed for accomplishing the software labs of the course. 

1. We can now log in to Satori with our favorite web browser:
    
    https://satori-portal.mit.edu
    
2. On "Interactive Apps" in the menu bar, click "Jupyter Notebook [Experimental]"
from the drop down menu.

3. Check all boxes and fill the two fields accordingly, using your own <mit_username>:

    Type path to Custom Anaconda Install
    
    `/nobackup/users/<mit_username>/projects/condas/IntroDeepLearningMIT/miniconda3/bin`
    
    Type Name of Custom Conda Environment
    
    `IntroDeepLearningMIT`
    
    
## Miscellaneous useful commands

List available conda environments:

```
conda info --envs
```

File transfer local machine --> remote machine:

```
scp <local-file.py> <mit_username>@satori-login-001.mit.edu:</your/remote/path/>
scp -r <local-repo> <mit_username>@satori-login-001.mit.edu:</your/remote/path/>
```

File transfer remote machine --> local machine:

```
scp <mit_username>@satori-login-001.mit.edu:<remote-file.py> </your/local/path/>
scp -r <mit_username>@satori-login-001.mit.edu:<remote-repo> </your/local/path/>
```

