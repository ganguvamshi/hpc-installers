## Installing mcl program

#### Downloading source file

```
cd /app1/centos6.3/source/
wget https://www.micans.org/mcl/src/mcl-latest.tar.gz
tar xvf mcl-latest.tar.gz -C ./mcl

```

#### Compile and install

```
cd mcl
./configure --prefix=/app1/bioinfo/mcl/14.137
make install

```
#### Create a Module file

create a text file using `vim` with the below content

```
#%Module -*****-
##
## modulefile
##
set name       vcftools
set version    0.1.15
set root       /app1/bioinfo/vcftools-0.1.15
set url        https://vcftools.github.io/index.html

proc ModulesHelp { } {
  global name
  global version
  global root
  global url
  puts stderr "\tAdds $name $version settings to your environment.\n\tPackage installed in $root\n\tFor usage type 'man bwa'\n\tMore information at $url\n"
}

module-whatis "adds $name version $version to your environment variables."


prepend-path      PATH              ${root}/bin
prepend-path      MANPATH           ${root}/share/man


```
now create the module directory for mcl and copy this file

```
mkdir -p /app1/modules/bioinfo/mcl
cp mod_mcl /app1/modules/bioinfo/mcl/14.137

```
Now the mcl is ready to use via `module`. you can load it using `module load mcl`