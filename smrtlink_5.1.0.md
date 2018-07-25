### Installing SMRT Link software

SMRT Link is the web-based end-to-end workflow manager for the Sequel® System. It includes software
applications for designing and monitoring sequencing runs, and analyzing and managing sequence data.
Additionally, SMRT Link provides support for multiple instruments. The Installation process is followed as instructed [here](http://programs.pacificbiosciences.com/l/1652/2018-03-20/3wrpm1/1652/190668/SMRT_Link_Software_Installation__v5.1.0_.pdf)

### Download software 

The needed run files are download along with the path run file.

```
cd /app1/bioinfo/source
mkdir smrtlink
wget https://downloads.pacbcloud.com/public/software/installers/smrtlink_5.1.0.26412.zip

unzip smrtlink_5.1.0.26412.zip

```

### Installation

This installation is carried out on venus06 directly. no need to be root.

#### environment variables 
env variables for easy installation purose.
```
bash

SMRT_ROOT=/hpctmp/biodata/smrtink/5.1.0
SMRT_USER=ccevg
SMRT_GROUP=svuusers

# Create Installation directory

mkdir -p $SMRT_ROOT
chown -R $SMRT_USER:$SMRT_GROUP $SMRT_ROOT
chmod -R 765 $SMRT_ROOT

```

#### Run the installation

```
./smrtlink_5.1.0.26412.run --rootdir $SMRT_ROOT

```