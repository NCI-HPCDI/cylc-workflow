# Guideline on setting up Cylc8 working environment

The purpose of this file is to configure your working environment on NCI's Gadi system for running the Clyc8 workflow

# Verify your cylc environment

Ensure that you have at least one active persistent session running. You can list all currently running persistent sessions by executing the following command on Gadi.

```
persistent-sessions list
```
Or you can start a new session via the following command in Gadi

```
persistent-sessions start YOUR_SESSION_NAME
```

## Step 1: Choose the ROSE_ORI_HOST

Starting the Cylc 8 workflow on Gadi can be done from the login node, a persistent session, or an ARE VDI session. However, for this exercise, it is recommended to open an ARE VDI session to run and monitor the Cylc 8 workflow.

Please refer to https://opus.nci.org.au/display/DAE/ARE+VDI+Sessions+for+Cylc+Jobs for instructions on starting an ARE VDI session.

Make sure you fill in the same default PROJECT id in the "Project" field. 

For example, if your default project id is "fp0", you should fill ```fp0``` in the "Project" field and fill ```gdata/ki32+gdata/hr22+gdata/access+gdata/fp0+scratch/fp0``` in the "Storage" field.

## Step 2: load the module

In your ARE VDI session, specify the persistent session name by setting the CYLC_SESSION environment variable or by placing it in the ~/.persistent-sessions/cylc-session file.

Then load the module as below

```
module use /g/data/hr22/modulefiles
module load cylc/8.2.1
```

## Step 3: execute the initialization step ( if you didn't run it)

```
/g/data/hr22/bin/gadi-cylc-setup-ps -y
```

After it, check the existence of the following 3 files under ~/.ssh directory

```
id_rsa-rose-cylc-gadi
id_rsa-rose-cylc-gadi-restricted.pub
id_rsa-rose-cylc-gadi.pub
```

## Step 4: verify your MOSRS account information

To enable access to the MOSRS, please execute the following command
```
mosrs-auth
```

## Step 5: checkout the test suite u-cz535

Now you can check out the test suite u-cz543 using the 'rosie co' command

```
 rosie co u-cz535
```
The suite runs the following tasks:

1. Cloning the source code of 'stream' by using the 'localhost' platform;
2. Building the 'stream' package  by using the 'pbs' platform;
3. Executing the 'stream' package  by using the 'pbs' platform;
    
## Step 6: execute the test suite u-cz535

The suite will be located at ~/roses/u-cz535. You can execute it using the 'rose suite-run' command.

```
cd ~/roses/u-cz535
cylc install
cylc play u-cz535
```

## Step 7: Monitor the job progress

You can only monitor the cylc8 workflow via an ARE VDI session.

Run the following command in ARE VDI which will open a web browser window"

```
cylc gui
```
Make sure all jobs can complete successfully.





