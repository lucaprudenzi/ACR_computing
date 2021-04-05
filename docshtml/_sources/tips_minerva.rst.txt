Useful tips for using Minerva
=============================

Quota
^^^^^

To find your current quota:

.. code-block:: bash 

    beegfs-ctl --getquota --uid $(id -u) --mount=/home
    beegfs-ctl --getquota --uid $(id -u) --mount=/work

Others
^^^^^^

(From Ian's collection of useful commands. TODO: tidy these up)

Using ethernet:

.. code-block:: bash

    export I_MPI_FABRICS=shm:tcp
    export I_MPI_TCP_NETMASK=enp7s0

Idle loaded nodes

.. code-block:: bash

    sinfo -p container -t idle -o "%n %O" -h|sort -k 2 -n|awk '$2 > 0.5 {print}'

Rogue processes

.. code-block:: bash

    for n in $(sinfo -p container -t idle -o %n -h);
        do 
        printf "%s\t%s\n" $n $(ssh -n $n ps -e -o comm= |grep -v 'supervisord\|slurmd\|rsyslogd\|sshd\|rsyslogd\|ps\|munged\|nslcd');
        done
    
    for n in $(sinfo -p container -t drain,idle -o %n -h);
        do
        printf "%s\t%s\n" $n $(ssh -n $n ps -e -o comm= |grep -v 'supervisord\|slurmd\|rsyslogd\|sshd\|rsyslogd\|ps\|munged\|nslcd');
        done

Active processes on each node

.. code-block:: bash

    while read node; do echo $node; ssh $node top -b -n 1 -i -d 10 </dev/null|tail -n +8; done <machines.txt

Job results

.. code-block:: bash

    sacct -S 2016-07-19 -u ian -o jobid,end,alloccpus,jobname%20,state|grep -v batch|sort -k 2

Reason nodes are in drain

.. code-block:: bash
    
    sinfo -o "%P %.5a %.10l %.6D %.6t %N %E"

    sinfo -p normal -t drain,down -o "%20H  %.40E: %N" | sort -r
    (with timestamps)

Nodes used by users

.. code-block:: bash

    squeue -a|awk '$5 == "R" {user = $4; nodes[user] += $7} END {for (u in nodes) {print u,nodes[u]}}'

Nodes in job c[109,135-141]

.. code-block:: bash

    for node in c109 c135 c136 c137 c138 c139 c140 c141;
        do
        echo $node; ssh $node top -b -n 1 -i -d 10 </dev/null|tail -n +8;
        done

Node list of a job

.. code-block:: bash

    squeue -j 37411 -o %N -h

Interactive job

.. code-block:: bash

    srun -N 1 --pty bash

Installing LALSimulation
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    git clone git@git.ligo.org:lscsoft/lalsuite.git
    cd lalsuite
    module load gsl/gcc/2.4
    export LIBRARY_PATH=/home/sossokine/sw/lib
    export CPATH=/home/sossokine/sw/include
    export PYTHONPATH=$PWD/lalsimulation/python:$PWD/lal/python/lal:$PYTHONPATH
    ./00boot
    ./configure --prefix ~/software/lalsuite --enable-all-lal=no --enable-lalsimulation=yes
    nice make -j 8
    make install
