# Guidelines for Establishing a Cylc 7 Working Environment on Gadi

This file is intended to configure your working environment on NCI Gadi for running the Cylc7 workflow in both localhost and accessdev-compatible modes. You could start your Cylc7 workflow from either a Gadi login node or a persistent session and leave it running at the persistent session. You could monitor Cylc 7 workflows anytime from a Gadi login node when it is still running.

# Prerequisite

Ensure that you have at least one active persistent session running. You could list all currently running persistent sessions via the following command on Gadi.

```
persistent-sessions list
```
Or you can start a new session via the following command on a Gadi login node

```
persistent-sessions start YOUR_SESSION_NAME
```

# Run Cylc7 suite from a persistent session

## Step 1: ssh to your activate persistent session.

Log into an active persistent session with X11 enabled so you can monitor the running Cylc7 workflow.

```
ssh -X gadi.nci.org.au
ssh -Y YOUR_PERSISTENT_SESSION_NAME.USER.PROJ.ps.nci.org.au

```

## Step 2: load the module

Load the following environment module. Since you are working within the persistent session, there is no need to specify the CYLC_SESSION environment variable or create the file ~/.persistent-sessions/cylc-session. The module will identify the current persistent session name and set it as CYLC_SESSION value.

```
module use /g/data/hr22/modulefiles
module load cylc7/23.09
```

The output should include a line like "Using the cylc session cylc.ab11.abc111.ps.nci.org.au," which indicates that the entire Cylc workflow will be pushed to this persistent session.


## Step 3: verify your MOSRS account information

To enable access to the MOSRS repository, you need to execute the following command and follow its operations.

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543

Now you can check out the test suite u-da543 using the 'rosie co' command
```
 rosie co u-da543
```

This suite offers two modes: Cylc7 'localhost' mode and 'accessdev-compatible' mode to run the following tasks:

1. Cloning the source code of 'stream' package using the 'background' batch system on the 'localhost' host (localhost mode).
2. Building the 'stream' package with the 'pbs' batch system on the 'localhost' host (localhost mode).
3. Executing the 'stream' package with the 'pbs' batch system on the 'gadi' host (Accessdev compatible mode).
 
## Step 5: execute suite u-da543

The suite will be located at ~/roses/u-da543. You can execute it with the 'rose suite-run' command.

```
cd ~/roses/u-da543
rose suite-run
```

A GUI window will appear to display the workflow's progress. 

If all jobs complete successfully, your are read to run Cylc7 suites in both 'localhost' and 'accessdev-compatible' modes from within the persistent session.

Now you need to exit the persistent session to continue this tutorial. Make sure the persistent session is still activating as we will use it in the next session.

# Run Cylc7 suite from Gadi login node

## Step 1: ssh to Gadi login node.

Ensure that you are on the Gadi login node and X11 is enabled. You could check it by executing following command and make sure a GUI clock can be displayed on your screen. 

```
xclock
```

Alternatively, you can initiate a new SSH login from your client computer via following ssh command.

```
ssh -X gadi.nci.org.au
```

## Step 2: load the module

Verify the existence of a file named "~/.persistent-sessions/cylc-session" or whether it contains the name of an active persistent session. If neither condition is met, you should assign an activate session name to the environment variable CYLC_SESSION, i.e.

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

It should display a message such as 'Using the cylc session cylc.ab11.abc111.ps.nci.org.au' to indicate the specific persistent session it will utilize.

## Step 3: verify your MOSRS account information

To enable access to the MOSRS, please execute the following command

```
mosrs-auth
```

## Step 4: run the suite u-da543 (check it out if it doesn't exist)

Run the following command to check out the suite if it does not already exist.

```
 rosie co u-da543
```

Now try to run the suite as below

```
cd ~/roses/u-da543
rose suite-clean
rose site-run
```
The suite can not start as it needs an extra step to run the "accessdev-compatible" mode, i.e. job with 'hosts=gadi', from the Gadi login node.    

## Step 5: execute the initialization step ( once only)

To run a Cylc7 suite in 'Accessdev compatible' mode, you should execute the following initialization script .

```
/g/data/hr22/bin/gadi-cylc-setup-ps -y
```

After it, check the existence of the following 3 files under ~/.ssh directory

```
id_rsa-rose-cylc-gadi
id_rsa-rose-cylc-gadi-restricted.pub
id_rsa-rose-cylc-gadi.pub
```
You only need to execute the above initialization step once.

Note: This initialization step is not required if you are running a Cylc7 suite in 'localhost' mode.

## Step 6: re-run the suite u-da543 

The suite will be stored in the directory ~/roses/u-da543. You can execute it using the 'rose suite-run' command. Prior to initiating a new run, ensure you clean it by using the 'rose suite-clean' command.

```
cd ~/roses/u-da543
rose suite-clean
rose site-run
```
A GUI window will appear to display the progress of the workflow. Ensure that all jobs can successfully complete. You can now run Cylc7 suites in both 'localhost' and 'accessdev-compatible' modes from the Gadi login node.





