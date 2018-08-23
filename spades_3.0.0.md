# SPAdes, dipSPAdes

## Downloading and installation

This is a binary installation, not from source.
```
mkdir /app1/bioinfo/spades
cd /app1/bioinfo/spades
wget http://spades.bioinf.spbau.ru/release3.0.0/SPAdes-3.0.0-Linux.tar.gz
tar -xzf SPAdes-3.0.0-Linux.tar.gz
mv SPAdes-3.0.0-Linux 3.0.0
```

## Modulefile

```
#%Module -*****-
##
## modulefile
##
set tool spades
set version 3.0.0
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


prepend-path        PATH                            ${prefix}/bin
```
