# nextflow 

A DSL for data-driven computational pipelines

## Download

download the latest exec file from github repo: <https://github.com/nextflow-io/nextflow>
here is the link: <https://github.com/nextflow-io/nextflow/releases/download/v19.01.0/nextflow>

## decompress, compile and install

Installation instructions. Java 1.8 is the only dependency required.

```
mkdir -p /app1/bioinifo/nextflow/19.01.0/bin
cd /app1/bioinifo/nextflow/19.01.0/bin
wget https://github.com/nextflow-io/nextflow/releases/download/v19.01.0/nextflow

# editing the NXF_HOME var in nextflow file

vim bin/nextflow
change the NXF_HOME line to NXF_HOME=${NXF_HOME:-/app1/bioinfo/nextflow/19.01.0/.nextflow}

# installation
module load jre/1.8.0_162
module load singularity
module load miniconda/3.6
./bin/nextflow # This will install dependencies at the first run

```

## Modulefile

the module file is as below:

```

# for Tcl script use only
set rkoversion      3.2.10
set url         http://www.nextflow.io
set nfdir       /hpctmp/biodata/nextflow-img



proc ModulesHelp { } {
        global rkoversion
        global name
        global version
        global root
        global url
        puts stderr "\tAdds $name (version $version) settings to your environment.\n\tMore information at $url"
}

module-whatis   "$name $version"
#module load /app1/modules/root/NUSREC

if { ![is-loaded jre/1.8.0_162] } {
        module load jre/1.8.0_162
}

if { ![is-loaded singularity] } {
        module load singularity
}

if { ![is-loaded miniconda/3.6] } {
        module load miniconda/3.6
}

prereq jre/1.8.0_162
prereq singularity
prereq miniconda/3.6

setenv  NXF_ASSETS                      $nfdir
setenv  NXF_CONDA_CACHEDIR              ~/.conda
setenv  NXF_SINGULARITY_CACHEDIR        ~/.singularity


prepend-path    PATH            ${root}/bin

if { [module-info mode load] } {
        puts stderr  "Welcome to Nexflow: Sample nextflow pipelines are located here:\n\t$nfdir\n\n"
}

```





