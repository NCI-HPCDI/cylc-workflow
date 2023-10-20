# Guideline on setting up Cylc7 working environment

The file aims to set up your working environment at NCI Gadi to run Clyc7 workflow in both localhost and accessdev compatible mode.

# Verify suite localhost mode

Make sure you alreay have at least one persistent session running. You can list all running persistent session via the command

```
persistent-sessions list
```

## Step 1: ssh to your alive persistent session.
```
ssh -X gadi.nci.org.au
ssh -Y YOUR_PERSISTENT_SESSION_NAME.USER.PROJ.ps.nci.org.au

```

## Step 2: load the module
As you are working within the persistent session, you don't need to specify the CYLC_SESSION environment variable or create the file  ~/.persistent-sessions/cylc-session

```
module use /g/data/hr22/modulefiles
module load cylc7/23.09
```

## Step 3: verify your MOSRS account information

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543

```
 rosie co u-da543
```

## Step 5: execute suite u-da543

```
cd ~/roses/u-da543
rose site-run
```

Make sure all jobs can complete successfully.


# Verify suite localhost mode

## Step 1: ssh to Gadi login node.

```
ssh -X gadi.nci.org.au
```

## Step 2: load the module

If there is no ~/.persistent-sessions/cylc-session file, or you want to use a different session name, you need to specify the session name via the environment variable as below

```
export CYLC_SESSION=NAME.USER.PROJ.ps.nci.org.au
```
For example,
```
export CYLC_SESSION=cylc.ab11.abc111.ps.nci.org.au
```
Then laod the module
```
module use /g/data/hr22/modulefiles
module load cylc7/23.09
```

## Step 3: execute the inilization step

```
/g/data/hr22/bin/gadi-cylc-setup-ps
```
After it, check whether the following 3 files are created under ~/.ssh directory

```
id_rsa-rose-cylc-gadi
id_rsa-rose-cylc-gadi-restricted.pub
id_rsa-rose-cylc-gadi.pub
```

# Step 4: verify your MOSRS account information

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543 you haven't done it.

```
 rosie co u-da543
```

## Step 5: execute suite u-da543

```
cd ~/roses/u-da543
rose suite-clean
rose site-run
```

Make sure all jobs can complete successfully.





