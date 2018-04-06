#  mysql installation


```
module load cmake boost/1.59.0 

cd /app1/centos6.3/sources/mysql-5.7.21

export LIBRARY_PATH=/app/centos6.3/gnu/boost/1.59.0/lib:$LIBRARY_PATH
export LD_LIBRARY_PATH=/app/centos6.3/gnu/boost/1.59.0/lib:$LD_LIBRARY_PATH
cmake -DCMAKE_INSTALL_PREFIX=/app1/centos6.3/gnu/mysql/5.7.21 -DBOOST_INCLUDE_DIR=/app1/centos6.3/gnu/boost/1.59.0/include -DMYSQL_DATADIR=/hpctmp/biodata/mysqldata -DMYSQL_UNIX_ADDR=/app1/centos6.3/gnu/mysql/mysql.sock -DENABLED_LOCAL_FILE=1 .
make -j5
make install

```


## mysql start and stop


_**start mysql service**_

`mysqld_safe --defaults-file="/hpctmp/biodata/mysqldata/mysql.cnf"`

_**stop mysql service**_

`mysqldadmin --defaults-file="/hpctmp/biodata/mysqldata/mysql.cnf" shutdown`
