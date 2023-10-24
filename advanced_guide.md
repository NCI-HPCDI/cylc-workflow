# Change deault cylc7 working directory in  ~/.metomi/rose.conf

For example, the following config will link ~/cylc-run towards /g/data and link the 'share' and 'work' subdirectories towards '/scratch'

```
[rose-suite-run]
root-dir=*=/g/data/$PROJECT/$USER
root-dir{share}=*=/scratch/$PROJECT/$USER
root-dir{work}=*=/scratch/$PROJECT/$USER
```
# Change deault cylc8 working directory in ~/.cylc/flow/global.cylc

For example, the following config will link 'log' subdirctory to '/g/data' and link the 'share' and 'work' subdirectories towards '/scratch'

```
#!Jinja2
[install]
    source dirs = ~/cylc-src, ~/roses
    [[symlink dirs]]
        [[[gadi]]]
            log = /g/data/{{environ['PROJECT']}}/{{environ['USER']}}
            share = /scratch/{{environ['PROJECT']}}/{{environ['USER']}}
            work = /scratch/{{environ['PROJECT']}}/{{environ['USER']}}
        [[[localhost]]]
            log = /g/data/{{environ['PROJECT']}}/{{environ['USER']}}
            share = /scratch/{{environ['PROJECT']}}/{{environ['USER']}}
            work = /scratch/{{environ['PROJECT']}}/{{environ['USER']}}
```

# Enable user script with remote connections

Put the following config into ~/.ssh/config will enable user script in the Rose/Cylc suite to connect to 'gadi' or 'gadi.nci.org.au'.
```
Host gadi.nci.org.au
   Match exec "echo '%l' | grep -q 'ps.gadi.nci.org.au'" host gadi,gadi.nci.org.au,localhost
        HostName localhost
	IdentityFile ~/.persistent-sessions/%l/user.key
	StrictHostKeyChecking no
	Port 2222
```