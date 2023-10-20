# Guideline on setting up Cylc8 working environment

The file aims to set up your working environment at NCI Gadi to run Clyc8 workflow.

# Verify your cylc environment

Make sure you alreay have at least one persistent session running. You can list all running persistent session via the command

```
persistent-sessions list
```

## Step 1: Choose the ROSE_ORI_HOST

You could initilize the cylc8 workflow from Gadi login node, persistent session or a ARE VDI session. It is recommanded to open an ARE VDI session in this excise to run and monitor the cylc8 workflow.

## Step 2: load the module

Specify the persistent session name via the environemnt varialbe CYLC_SESSION environment variable or put it in the file  ~/.persistent-sessions/cylc-session

Load the module as below

```
module use /g/data/hr22/modulefiles
module load cylc8/8.2.1
```

## Step 3: verify your MOSRS account information

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543

```
 rosie co u-cz535
```

## Step 5: execute suite u-da543

```
cd ~/roses/u-cz535
cylc install
cylc play u-cz535
```

Make sure all jobs can complete successfully.

## Step 6: Monitor the job progress

You can only monitor the cylc8 workflow via an ARE VDI session.





