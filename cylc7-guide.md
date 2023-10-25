# Guideline on setting up Cylc7 working environment

This file is intended to configure your working environment on NCI Gadi for running the Cylc7 workflow in both localhost and accessdev-compatible modes.

# Run Cylc7 suite from a persistent session

Ensure that you have at least one active persistent session running. You can list all currently running persistent sessions by executing the following command on Gadi.

```
persistent-sessions list
```
Or you can start a new session via the following command in Gadi

```
persistent-sessions start YOUR_SESSION_NAME
```

## Step 1: ssh to your alive persistent session.

Log into an active persistent session with X11 enabled so you can monitor the running Cylc7 workflow.
```
ssh -X gadi.nci.org.au
ssh -Y YOUR_PERSISTENT_SESSION_NAME.USER.PROJ.ps.nci.org.au

```

## Step 2: load the module

Load the following module. Since you are working within the persistent session, there is no need to specify the CYLC_SESSION environment variable or create the file ~/.persistent-sessions/cylc-session.

```
module use /g/data/hr22/modulefiles
module load cylc7/23.09
```

The output will include a line such as "Using the cylc session cylc.ab11.abc111.ps.nci.org.au," which indicates that you will be pushing your entire Cylc workflow to this persistent session.


## Step 3: verify your MOSRS account information

To enable access to the MOSRS, please execute the following command

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543

Now you can check out the test suite u-da543 using the 'rosie co' command
```
 rosie co u-da543
```

The suite offers two modes: Cylc7 localhost mode and Accessdev compatible mode for running the following tasks:

1. Cloning the source code of 'stream' using the 'background' batch system on the 'localhost' host (localhost mode).
2. Building the 'stream' package with the 'pbs' batch system on the 'localhost' host (localhost mode).
3. Executing the 'stream' package with the 'pbs' batch system on the 'gadi' host (Accessdev compatible mode).
 
## Step 5: execute suite u-da543

The suite will be located at ~/roses/u-da543. You can execute it using the 'rose suite-run' command.

```
cd ~/roses/u-da543
rose suite-run
```
A GUI window will appear to display the workflow's progress. Ensure that all jobs can successfully complete.

Now you can run both Cylc7 in localhost and accessdev compatible modes from within the persistent session.

You can exit the persistent session, but please do not terminate it as we will use it in the next session.

# Run Cylc7 suite from Gadi login node

## Step 1: ssh to Gadi login node.

Ensure that you are on the Gadi login node and that X11 is enabled.

Alternatively, you can initiate a new SSH login using the following command.

```
ssh -X gadi.nci.org.au
```

## Step 2: load the module

Verify the existence of a file named "~/.persistent-sessions/cylc-session" or whether it contains the name of the active persistent session. If neither condition is met, you should set the session name using the environment variable CYLC_SESSION, i.e.

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

It will display information such as 'Using the persistent session cylc.ab11.abc111.ps.nci.org.au' to indicate the specific persistent session it will utilize.

## Step 3: execute the initialization step ( once only)

To run a Cylc7 suite in Accessdev compatible mode, you should execute the following initialization script.

```
/g/data/hr22/bin/gadi-cylc-setup-ps
```

After it, check the existence of the following 3 files under ~/.ssh directory

```
id_rsa-rose-cylc-gadi
id_rsa-rose-cylc-gadi-restricted.pub
id_rsa-rose-cylc-gadi.pub
```
You only need to execute the initialization step provided above once.

This initialization step is not required if you are running a Cylc7 suite in localhost mode.

## Step 4: verify your MOSRS account information

To enable access to the MOSRS, please execute the following command

```
mosrs-auth
```

## Step 5: checkout the test suite u-da543 if you haven't done it.

You can now check out the 'u-da543' test suite using the 'rosie co' command if the suite does not already exist.

```
 rosie co u-da543
```

## Step 6: execute suite u-da543

The suite will be stored in the directory ~/roses/u-da543. You can execute it using the 'rose suite-run' command. Prior to initiating a new run, ensure you clean it by using the 'rose suite-clean' command.

```
cd ~/roses/u-da543
rose suite-clean
rose site-run
```
A GUI window will appear to display the progress of the workflow. Ensure that all jobs can successfully complete. You can now run Cylc7 in both localhost and accessdev-compatible modes from the Gadi login node.





