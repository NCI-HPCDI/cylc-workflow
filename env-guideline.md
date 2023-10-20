# cylc env guideline at Gadi
The file aims to set up your working environment at NCI Gadi to run Clyc7 workflow in both localhost and accessdev compatible mode.

# Verify suite localhost mode

## Step 1: ssh to your alive persistent session.
```
ssh -X gadi.nci.org.au
ssh -Y YOUR_PERSISTENT_SESSION_NAME.USER.PROJ.ps.nci.org.au

```

## Step 2: load the module
As you are working within the persistent session, you don't need to specify the CYLC_SESSION environment or create the cylc

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
