# Steps for installing reference data for Orthomcl using _mysql_

Here are the steps to install orthomcl reference database using mysql for dm6 (UP000000803) from Uniprot.

#### Data directory

create a seperate directory and download the dm6 protein reference fasta file.

```
mkdir /hpctmp/biodata/mysqldata/orthomcl/dm6_UP000000803
cd /hpctmp/biodata/mysqldata/orthomcl/dm6_UP000000803
```
An orthomcl config file has to be generated with relevant mysql configuration. You can makee use of sample conf file that comes along with orthomcl source file as a reference. here our config file `orthomcl.config` is present in the same data directory.

##### download dm6 proteome fasta from Uniprot ftp

```
wget ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/reference_proteomes/Eukaryota/UP000000803_7227.fasta.gz

```
#### Load required modules and start mysql service

```
module load mysql/5.7.21_test orthomcl/2.0.9 mcl/14.137

#start mysql service
mysqld_safe --defaults-file="/hpctmp/biodata/mysqldata/mysql.cnf"

```

## Orthmcl Steps

### 1. orthomclInstallSchema
`orthomclInstallSchema orthomcl.config install_schema.log`
### 2. orthomclAdjustFasta
`orthomclAdjustFasta dm6 /hpctmp/biodata/mysqldata/orthmcl/UP000000803_7227.fasta 2`
### 3. orthomclFilterFasta
`orthomclFilterFasta $PWD  10 20`
### 4. All-v-all Blast
```
makeblastdb -in goodProteins.fasta -dbtype prot -out dm6_blastdb
blastp -db dm6_blastdb -query fasta/goodProteins.fasta  -evalue 1e-5 -outfmt 6 -num_threads 6 -out dm6_all-v-all_blast.tsv

```
### 5.orthomclBlastParser
`orthomclBlastParser dm6_all-v-all_blast.tsv fasta/ >>smilarSequences.txt`
### 6. orthomclLoadBlast
`orthomclLoadBlast orthomcl.config smilarSequences.txt`
### 7. orthomclPairs
`orthomclPairs orthomcl.config orthomclpairs.log cleanup=yes`
### 8. orthomclDumpPairsFiles
`orthomclDumpPairsFiles orthomcl.config`
### 9. mcl
```
module load mcl/14.137
mcl mclInput --abc -I 1.5 -o mclOutput
```
### 10. orthomclMclToGroups
`orthomclMclToGroups dm6 1000 <mclOutput >groups.txt`


## Now stop the mysql service 

After finishing all the orhomcl commands, now we should stop the mysql service as below

`mysqldadmin --defaults-file="/hpctmp/biodata/mysqldata/mysql.cnf" shutdown`