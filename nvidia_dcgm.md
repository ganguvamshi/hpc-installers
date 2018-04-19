# Installing the Nvidia GPU DCGM tool within gpu server

Now testing the installation in one node

`/hpctmp/root/downloads/Nvidia/nvidia-diag-driver-local-repo-rhel6-384.66-1.0-1.x86_64.rpm`

Installing the package using rpm

```
rpm -Uvh nvidia-diag-driver-local-repo-rhel6-384.66-1.0-1.x86_64.rpm`

## generated output:
warning: nvidia-diag-driver-local-repo-rhel6-384.66-1.0-1.x86_64.rpm: Header V3 RSA/SHA512 Signature, key ID 7fa2af80: NOKEY
Preparing...                ########################################### [100%]
   1:nvidia-diag-driver-loca########################################### [100%]

```

#### Installing drivers using Run file as gpu nodes doesnt have internet access
becuase of internet issue, we cant directly use the rpm installtin. download the Nvidia drivers for cuda8 for general Linux x86_64

```
sh NVIDIA-Linux-x86_64-384.66.run 
# this will install the 384 driver in the node, replacing any exisiting drivers

rpm -ivh datacenter-gpu-manager-1.3.3-1.x86_64.rpm
Preparing...                ########################################### [100%]
   1:datacenter-gpu-manager ########################################### [100%]

```




### Testing 

Testing the installation 

```
nv-hostengine
Started host engine version 1.3.3 using port number: 5555 

# list all the gpus

dcgmi discovery -l
```






