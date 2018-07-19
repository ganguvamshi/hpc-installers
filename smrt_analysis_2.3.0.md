### Installing SMRT Analysis software

SMRT Analysis software is used to process, analyze sequencing data from pacbio technology. The Installation process is followed as instructed [here](https://www.pacb.com/wp-content/uploads/SMRT-Analysis-Software-Installation-v2-3-0.pdf)

### Download software 

The needed run files are download along with the path run file.

```
cd /app1/bioinfo/source
mkdir smrt_analysis
wget https://s3.amazonaws.com/files.pacb.com/software/smrtanalysis/2.3.0/
wget https://s3.amazonaws.com/files.pacb.com/software/smrtanalysis/2.3.0/smrtanalysis-patch_2.3.0.140936.p5.run

```

### Installation

#### environment variables 
env variables for easy installation purose.
```
SMRT_ROOT=/app1/bioinfo/smrt/2.3.0/
SMRT_USER=ccevg
SMRT_GROUP=svuusers

# Create Installation directory

mkdir -p $SMRT_ROOT
chown -R $SMRT_USER:$SMRT_GROUP $SMRT_ROOT
chmod -R 765 $SMRT_ROOT

```

#### Run the installation

```
 su -l $SMRT_USER
bash  smrtanalysis_2.3.0.140936.run -p smrtanalysis-patch_2.3.0.140936.p5.run --rootdir $SMRT_ROOT

```