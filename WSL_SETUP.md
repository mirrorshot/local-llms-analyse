# Running the notebooks in WSL

## Initialize environment

This is a list of preliminary configurations to the environment, to be applied if not already active.

### Net tools

As we are going to need the WSL ip to refer to it from the IDE, command `ifconfig` is needed 
and can be installed via:
```shell
sudo apt install net-tools
```

### Expose Ollama to outside WSL

To make Ollama available http service accessible from the host machine, 
edit `/etc/systemd/system/ollama.service` and add in the `[Service]` section.
```
Environment="OLLAMA_HOST=0.0.0.0"
Environment="OLLAMA_ORIGINS=*"
```

Then restart _Ollama_ running:
```shell
sudo systemctl restart ollama.service
```

## Install CONDA

Use the following commands to install MiniConda on the WSL machine
```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
rm Miniconda3-latest-Linux-x86_64.sh
```

To have `conda` command available through all the environment, you can run
```shell
sudo ln -L <installation_path>/bin/conda /bin/conda
```

Create a custom _conda_ environment for the project
```shell
conda env create -f conda_env.yml
```
Activate the conda environment
```shell
conda activate <environment-name>
```
The default environment name is `expense-analysis`

## Setup Jupyter

Prepare a directory where _Jupyter Lab_ will operate su as:
```shell
cd ~
mkdir expenses-jupyter
cd expenses-jupyter
mkdir lab
cd lab
```

### Start Jupyter Lab
Within the conda environment, run:
```shell
cd <jupyter lab directiory>
jupyter lab --no-browser --ip=0.0.0.0 2>../jupyter_lab.log
```
