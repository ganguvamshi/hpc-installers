# Gridss

the binary jar file can be used without compiling from source. Requires java 1.8. R and bwa

## Download and install

```
cd /app1/bioinfo
mkdir -p ./gridss/bin && cd gridss
wget -O gridss-jar-with-dependencies.jar https://github.com/PapenfussLab/gridss/releases/download/v1.8.1/gridss-1.8.1-gridss-jar-with-dependencies.jar

mv gridss-jar-with-dependencies.jar ./bin
```



## Modulefile

depends on jre1.8, R and bwa

```
#%Module -*****-
##
## modulefile
##
set tool gridss
set version 1.8.1
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n You can run it as java -Xmx12G \$GRIDSS_JVM_ARGS -cp \$GRIDSS_JAR"


if { ![is-loaded R-3.2.5 ] } {
        module load R-3.2.5
}

if { ![is-loaded jre/1.8.0_162 ] } {
        module load jre/1.8.0_162
}

if { ![is-loaded bwa/0.7.17 ] } {
        module load bwa/0.7.17
}

if { ![is-loaded samtools/1.6 ] } {
        module load samtools/1.6
}

prereq R-3.2.5
prereq jre/1.8.0_162
prereq bwa/0.7.17
prereq samtools/1.6

set                     GRIDSS_JAR                      ${prefix}/bin/gridss-1.8.1-jar-with-dependencies.jar
set                     GRIDSS_JVM_ARGS                 "-Dsamjdk.use_asyncio_read_samtools=true -Dsamjdk.use_async_io_write_samtools=true -Dsamjdk.use_async_io_write_tribble=true -ea"

setenv                  GRIDSS_JAR                      ${GRIDSS_JAR}
setenv                  GRIDSS_JVM_ARGS                 ${GRIDSS_JVM_ARGS}

if { [ module-info mode load ] } {
        puts stderr "you can run gridss using this command:\n java -Xmx12G \$GRIDSS_JVM_ARGS -cp $GRIDSS_JAR"
```