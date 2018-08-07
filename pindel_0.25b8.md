# Pindel Installation

Pindel can detect breakpoints of large deletions, medium sized insertions, inversions, tandem duplications and other structural variants at single-based resolution from next-gen sequence data. It uses a pattern growth approach to identify the breakpoints of these variants from paired-end short reads.

## Download 
```
cd /app1/bioinfo/source/git
git clone git://github.com/genome/pindel.git
```

## Compile and Install

This require htslib for compilation

```
cd pindel
./INSTALL /app1/bioinfo/htslib/1.8/
mkdir -p /app1/bioinfo/pindel/0.25b8/bin
cp -v pindel sam2pindel pindel2vcf* /app1/bioinfo/pindel/0.25b8/bin

```

## Modulefile

```
#%Module -*****-
##
## modulefile
##
set tool pindel
set version 0.25b8
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


prepend-path        PATH                            ${prefix}/bin
```