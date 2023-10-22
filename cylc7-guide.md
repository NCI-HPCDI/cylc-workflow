# Guideline on setting up Cylc7 working environment

The file aims to set up your working environment at NCI Gadi to run Clyc7 workflow in both localhost and accessdev compatible mode.

# Run Cylc7 suite from a persistent session

Make sure you alreay have at least one persistent session running. You can list all running persistent session by executing the command in Gadi. 

```
persistent-sessions list
```
You can start a new session via the following command in Gadi:

```
persistent-sessions start YOUR_SESSION_NAME
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

The output will display a line like "Using the cylc session mytest.jpf777.fp0.ps.gadi.nci.org.au", which indicates you will push all your cylc workflow to this persistent session. 


## Step 3: verify your MOSRS account information

You need to run the following command to enable the access towards MOSRS repo.

```
mosrs-auth
```

## Step 4: checkout the test suite u-da543

Now you can check out the test suitle u-da543 via 'rosie' command
```
 rosie co u-da543
```
The suite contains both Cylc7 localhost mode and accessdev compatible model.

## Step 5: execute suite u-da543

The suite will be stored under ~/roses/u-da543. You could run it with "rose suite-run" command.

```
cd ~/roses/u-da543
rose site-run
```
A GUI window will pop up to show the progres sof the workflow. Make sure all jobs can complete successfully and you can run both Cylc7 localhost and accessdev compatible modes from within the persistent session.

You can quit the persistent session and go back to the Gadi login node. Don't kill the persistent session.

# Run Cylc7 suite from Gadi login node

Make sure you are in the Gadi login node and the X11 is enabled.

You could also start a new ssh login as below.

## Step 1: ssh to Gadi login node.

```
ssh -X gadi.nci.org.au
```

## Step 2: load the module

Check whether a file named "~/.persistent-sessions/cylc-session" exists or whether it contains the persistent session name which is alive. In neither is true, you need to specify the session name via the environment variable CYLC_SESSION, i.e.

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
It will display the information like "Using the cylc session cylc.ab11.abc111.ps.nci.org.au" to indicate which persistent session it will use.

## Step 3: execute the initialization step ( once only)

You need to run the following Initialization script to run Cylc7 suite in accessdev compatbile mode.

```
/g/data/hr22/bin/gadi-cylc-setup-ps
```

After it, check the existence of the following 3 files under ~/.ssh directory

```
id_rsa-rose-cylc-gadi
id_rsa-rose-cylc-gadi-restricted.pub
id_rsa-rose-cylc-gadi.pub
```
You only need to run the above initialization step once. 

Note: You don't need the above inilization step if you are running Cylc7 suite in localhost mode.


# Step 4: verify your MOSRS account information

You need to run the following command to enable the access towards MOSRS repo.
```
mosrs-auth
```

## Step 4: checkout the test suite u-da543 you haven't done it.
Now you can check out the test suitle u-da543 via 'rosie' command if the suite doesn't exist.

```
 rosie co u-da543
```

## Step 5: execute suite u-da543
The suite will be stored under ~/roses/u-da543. You could run it with "rose suite-run" command. Make sure to clean it via "rose suite-clean" command before making a new run

```
cd ~/roses/u-da543
rose suite-clean
rose site-run
```
A GUI window will pop up to show the progres sof the workflow. Make sure all jobs can complete successfully and now you can run both Cylc7 localhost and accessdev compatible modes from within the Gadi login node.





