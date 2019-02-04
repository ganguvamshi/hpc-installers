# Installing QETLAB

downloding _QETLAB_

```
mkdir -p ~/matlab_scripts & cd ~/matlab_scripts 
wget https://github.com/nathanieljohnston/QETLAB/archive/v0.9.tar.gz
tar xvf v0.9.tar.gz
cd QETLAB-0.9
addpath(genpath("~/matlab_script/QETLAB-0.9")
```
the addpath is covered in the last section

# Installing CVX

creating scripts directory and download cvx

```
cd ~/matlab_scripts
wget http://web.cvxr.com/cvx/cvx-a64.tar.gz
tar -xvf cvx-a64.tar.gz
cd cvx

# open matlab in GUI/command-line mode in this cvx folder

matlab -nodisplay -nosplash # (command-line option)
addpath(genpath("~/matlab_scripts/QETLAB-0.9"))
cvx_setup
# if you have professional license and saved inside licenses folder within cvx directory.

cvx_setup ./licenses/cvx_license.mat

```

below is the sample installation status which show about the installed solvers. _SDPT3_ and _SeDuMi_ are included in the package. A professional license is required for _Gurobi_ and _Mosex_ solvers ref: <http://cvxr.com/cvx/doc/install.html#solvers-included-with-cvx>


```
---------------------------------------------------------------------------
CVX: Software for Disciplined Convex Programming       (c)2014 CVX Research
Version 2.1, Build 1127 (95903bf)                  Sat Dec 15 18:52:07 2018
---------------------------------------------------------------------------
Installation info:
    Path: /home/svu/ccevg/matlab_scripts/cvx
    MATLAB version: 9.4 (R2018a)
    OS: Linux amd64 version 2.6.32-696.18.7.el6.x86_64
    Java version: 1.8.0_144
Verfying CVX directory contents:
    No missing files.
Preferences: none found; defaults loaded.
License host:
    Username: ccevg
    Host ID: 487b6b4bef3e (eth0,172.19.119.11,172.25.195.51)
Installed license:
    No license installed.
No valid licenses found.
    <a href=<http://cvxr.com/cvx/academic?c_act=fill&c_unm=ccevg&c_hid=487b6b4bef3e
">Click here</a> to fill out an academic license request
    for the username and first hostid listed above.
---------------------------------------------------------------------------
Setting CVX paths...done.
Saving updated path...failed. (see below)
Searching for solvers...5 shims found.
2 solvers initialized (* = default):
 *  SDPT3    4.0         {cvx}/sdpt3
    SeDuMi   1.34        {cvx}/sedumi
3 solvers skipped:
    GLPK                 
        Could not find a GLPK installation.
    Gurobi   unknown     {cvx}/gurobi/a64
        Undefined function 'my_get_report' for input arguments of type
            'MException'.
    Mosek    8.0.0.60    {cvx}/mosek/a64
        Using MOSEK with CVX requires an academic MOSEK license
        or a MOSEK-enabled CVX Professional license.
Saving updated preferences...done.
Testing with a simple model...done!
---------------------------------------------------------------------------
To change the default solver, type "cvx_solver <solver_name>".
To save this change for future sessions, type "cvx_save_prefs".
Please consult the users' guide for more information.
---------------------------------------------------------------------------
NOTE: the MATLAB path has been changed to point to the CVX distribution. To
use CVX without having to re-run CVX_SETUP every time MATLAB starts, you
will need to save this path permanently. This script attempted to do this
for you, but failed---likely due to UNIX permissions restrictions.
To solve the problem, create a new file
    /home/svu/ccevg/Documents/MATLAB/startup.m
containing the following line:
    run /home/svu/ccevg/matlab_scripts/cvx/cvx_startup.m
Then execute the following MATLAB commands:
    userpath reset; startup
Please consult the MATLAB documentation for more information about the
startup.m file and its proper placement and usage.
---------------------------------------------------------------------------
```
ignore the path setting for now. It is covered in the last section

# Installing SDPT3

__SDPT3 4.0__ is already installed within CVX. you can just type `cvx_solver sdpt3` to use `sdpt3` within CVX

<http://web.cvxr.com/cvx/doc/solver.html>

# Installing YALMIP

Download 

```
cd ~/matlab_scripts
wget -O yalmip.zip https://github.com/yalmip/YALMIP/archive/master.zip
unzip yalmip.zip
mv -v YALMPI-master YALMIP
cd YAMLIP
```
For using YALMIP, you just need to add YALMIP dir to MATLAB path

```
matlab -nodesktop -nosplash
addpath(genpath("~/matlab_scripts/YALMIP"))
```
This path can be added using startup file (see below)


# using _startup.m_ file for reusability of all packages

create a startup.m file in your working dir and add the below lines to it to use CVX, YALMIP, QETLAB

```
run ~/matlab_scripts/cvx/cvx_startup.m
addpath ~/matlab_scripts/QETLAB-0.9
addpath ~/matlab_scripts/YALMIP
```

change the toolbox directory paths accordingly. 

open **MATLAB** (`matlab -nodesktop -nosplash`) and type `startup` to use all the above packages. 

