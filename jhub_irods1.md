# Installing JuputerHub in irods1 server

## Prepare conda environment for Jhub

Miniconda is installed in irdos1 root environment for this. a conda env named jhubconda is created with all jhub dependencies

```
ssh irods1
module load miniconda
conda create --prefix=/app1/datascience/jhub-irods1/condaenvs/jhubconda jupyterhub
source activate /app1/datascience/jhub-irods1/condaenvs/jhubconda
# install required spawners 
pip install git+https://github.com/jupyterhub/wrapspawner
pip install batchspawner
pip install jupyterhub-singularity-spawner
pip install dockerspawner

# install authenticator
conda install -c conda-forge jupyterhub-ldapauthenticator 

## installing rstudio server
conda install -c r/label/borked rstudio
conda install -c conda-forge  nbrsessionproxy

conda install -c bioconda singularity 
```

## Folders and file locations

- `/srv/jupyterhub` for all security and runtime files
- `/etc/juputerhub` for all configuration files
- `/var/log` for all log files

`mkdir /etc/juputerhub /srv/jupyterhub`


## Configurtion

In this section

### Generate default config file

Jhub will look for a conf file: `jupyterhub_config.py` in the current working dir

```
jupyterhub --generate-config
mv -v ./jupyterhub_config.py /etc/jupyterhub/
```


