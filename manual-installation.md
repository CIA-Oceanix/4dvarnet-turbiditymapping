# Install environment

---
## Tested environment

List of [environments that have been tested](./environment-tested.md), and validated where possible.

---
## Get repository

``` bash
git clone https://gitlab.imt-atlantique.fr/edito/4dvarnet-turbiditymapping.git
cd 4dvarnet-turbiditymapping
```

---
## Conda configuration

### Check if conda is available

Display conda version
``` bash
conda --version 
``` 

If a version is displayed, you can directly go to "Install dependencies".

If not, you need to install conda in your local laptop or homedir in a server, to manage python environment.


### Install conda 

 ```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -p $HOME/miniconda3 
# Done with installing conda here!
```
After this a directory will be created to contain all library of conda

### Check Conda environment

Now let’s check whether we have conda or not:
```bash
bash (this is to change to Bash mode)
conda --version in case we want to check the version
eval "$(/home/local-user/miniconda3/condabin/conda shell.bash hook)" (please change the directory to yours)
conda init
```

### Install conda on Google Collab

``` bash
pip install --quiet condacolab
```

---
## Install dependencies


### Important : PyTorch and Associated Libraries and CUDA Version

Python dependencies are installed using the `environment.yaml` file.

For PyTorch-CUDA, to avoid conflicts, do not install another version of PyTorch-CUDA if it is already installed.

Instead, make sure to remove any PyTorch-CUDA entries from the environment.yaml file, and to ensure compatibility with the CUDA version installed you need to install PyTorch, torchvision, and torchaudio using a specific CUDA version.

You can get the exact version with the command on the terminal of the system:
``` bash
echo $CUDA_VERSION
```

Note : If you are using Docker or Singularity/Apptainer, you can use the `inseefrlab/onyxia-jupyter-pytorch:py3.11.10-gpu` image.


### Initialyse Python environment

``` bash
cd /home/onyxia/work/ (in order to install the new environment here - please change the directory to yours)

conda install -c conda-forge mamba

conda create -n 4dvarnet
# conda create -n 4dvarnet mamba python=3.9 -c conda-forge
conda activate 4dvarnet
mamba env update -y -f environment.yaml (please change the directory to yours)
mamba clean -a
```

If the PyTorch-CUDA was already installed in ypour environment, and you have removed y=them from the `environment.yaml` file, use  this command to install PyTorch, pytorch-lightning, torchvision, and torchaudio libraries, ensuring they are built the right CUDA version support (12.2 in this exemple) :
```bash
mamba install -y pytorch  pytorch-lightning torchvision torchaudio pytorch-cuda=12.2 -c pytorch -c nvidia
mamba clean -a
```

If you get somme error messages, have a look at the "[known-issues](./known-issues.md)" documentation. In some situations, the version of numpy, or component used by pyTorch must be adapted.

You also may need to install ipython and omegaconfig :
``` bash
mamba install ipykernel omegaconfig
```

---
## Run JupyterLab 

1. Start Jupyterlab
``` bash
jupyter lab --no-browser --ip 0.0.0.0
```
2. Connect to the jupyter session : [http://localhost:8888](http://localhost:8888)



