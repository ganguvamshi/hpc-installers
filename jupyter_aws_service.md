## Jupyter as a system service


Setting up jupyter noteboko server as a service 


### Step 1: jupyter location

verify the jupyter notebook location:
```
$ ll ~/.local/bin/jupyter-notebook

```

### Step 2: Jupyter config file

Configure your notebook with password and ip address as needed and make sure where it exist. We will use this file as a coniguraton for jupyter as a service

```
jupyter config: ~/.jupyter/jupyter_notebook_config.py
```

### Step 3: Creating a jupyter service

Create a file name __jupyter.service__ as below and save it into __`/usr/lib/systemd/system/`__ folder

```
$ cat /usr/lib/systemd/system/jupyter.service
[Unit]
Description=Jupyter notebook

[Service]
Type=simple
PIDFile=/run/jupyter.pid 
# Step 1 and Step 2 details are here..
# ------------------------------------
ExecStart=/home/avkash/.local/bin/jupyter-notebook --config=/home/avkash/.jupyter/jupyter_notebook_config.py
User=avkash
Group=avkash
WorkingDirectory=/home/avkash/tools/notebooks
Restart=always
RestartSec=10
#KillMode=mixed

[Install]
WantedBy=multi-user.target

```
### Step 4: Enable the jupyter service now

```
$ sudo systemctl enable jupyter.service
```

### Step 5: reload the systemctl daemon

```
$ sudo systemctl deamon-reload
```

### Step 6: Restart the jupyter service
```
$ sudo systemctl restart jupyter.service
```

Jupyter service is started now. You can test it as below

```
$ systemctl -a |grep jupyter
jupyter.service         loaded active running Jupyter notebook

```

