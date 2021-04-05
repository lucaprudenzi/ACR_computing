First steps on Minerva
======================

Logging in
^^^^^^^^^^

Minerva can be reached via ssh to one of two login nodes, which are known by DNS as **minerva01.aei.mpg.de** and **minerva02.aei.mpg.de**. Internally, their names are **login01** and **login02**.

- Learn how to type “minerva” without mixing the letters.
- Find the private counterpart of the submitted public key.
- Setup a couple of entries in your **.ssh/config** file, to make typing easier, and use the correct key.

Once logged in, you can access the other login node, and the compute nodes (**node[001-594]**) by passwordless ssh - a special keypair without passphrase has been created and installed for you. **Do not use this key outside of Minerva**.

Slurm Basics
^^^^^^^^^^^^^

See `Slurm's Rosetta Stone <http://slurm.schedmd.com/rosetta.pdf>`_

Here's a script file stolen from CV:

.. code-block:: bash

    #!/bin/bash

    #SBATCH -J imb-03
    #SBATCH -N 412
    #SBATCH --ntasks-per-node 16
    #SBATCH -t 20
    #SBATCH -m cyclic:cyclic
    #SBATCH -D /home/cvsupport/dmitry/benchmarks/imb/03
    #SBATCH -o %N.%j.%a.out
    #SBATCH -e %N.%j.%a.err

    echo $SLURM_JOB_NODELIST

    module purge
    module load intel2016.3/mpi/64/5.1.3
    export I_MPI_DEBUG=5
    export I_MPI_FABRICS=shm:tmi
    export I_MPI_FALLBACK=no
    #export I_MPI_PIN=yes
    #export I_MPI_PIN_PROCESSOR_LIST=8

    mpirun -genvall -n $(($SLURM_JOB_NUM_NODES*$SLURM_NTASKS_PER_NODE)) -rr ../IMB-MPI1.intel2016.3 -multi 1 PingPing

Someone willing to comment, and explain the details?


Interactive sessions
^^^^^^^^^^^^^^^^^^^^
- `salloc -p devel` will submit a job to the selected partition
- if there are free resources (and you're allowed to use them!), this starts a new shell on the login node and assigns the requested resources
- you may check using `env | grep SLURM`

.. code-block:: bash

    [stefgru@login01 ~]$ env | grep SLURM
    SLURM_NODELIST=node579
    SLURM_JOB_NAME=bash
    SLURM_NODE_ALIASES=(null)
    SLURM_NNODES=1
    SLURM_JOBID=39809
    SLURM_TASKS_PER_NODE=16
    SLURM_JOB_ID=39809
    SLURM_SUBMIT_DIR=/home/stefgru
    SLURM_JOB_NODELIST=node579
    SLURM_CLUSTER_NAME=minerva
    SLURM_JOB_CPUS_PER_NODE=16
    SLURM_SUBMIT_HOST=login01.cluster
    SLURM_JOB_PARTITION=devel
    SLURM_JOB_NUM_NODES=1

- you're still on te login node, `srun` will use the allocated node(s) (recommendation: start screen to have access to the node(s) in parallel)
- `exit` will close the session, and return the allocated node(s) to the pool

It is recommended to use IntelMPI (IMPI) with Slurm (*that's what PIK people say*). Slurm and IMPI will do the correct binding for you, with OpenMPI you may see strange effects.

(to be extended) 
