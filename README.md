# equinox mit
Contains code that process mitgcm output for the EQUINOx project

- sandbox/ : first trials with xmitgcm, basic stuff

- launch/ : scripts required to launch jupyterlabs  and dask clusters

- doc/ : conda and git info

---
## install

All scripts require python librairies that may be installed with conda according to the following instructions [here](https://github.com/apatlpo/mit_equinox/blob/master/doc/conda.md)

---
## run on datarmor:

After having installed all libraries, and cloned this repository, go into `mit_equinox/datarmor`.

### method 1 (preferred):

```
./launch-jlab.sh
```

Follow instructions that pop up from there.

The spin up of dask relies on dask-jobqueue:
```
from dask_jobqueue import PBSCluster
cluster = PBSCluster()
w = cluster.start_workers(28*2)

from dask.distributed import Client
client = Client(cluster)
```

Kill jobs once done with computations in  a notebook with:
```
cluster.close()
```
or in a shell with `python kill.py`.

Clean up after computations: `./clean.sh`

### method 2 :

For 8 nodes for example:
```
./launch-dask.sh 8
./launch-jlab.sh wait
```

Follow instructions that pop up from there

Once you are done computing, kill the relevant jobs.

Clean up after computations: `./clean.sh`
