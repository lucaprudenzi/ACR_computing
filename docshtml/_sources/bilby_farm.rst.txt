The "Bilby Farm"
================

Hypatia, like its predecessors Merlin, Morgane and Vulcan, uses the `HTCondor scheduler <https://research.cs.wisc.edu/htcondor>`_ which is optimized for "narrow" HTC tasks but has a couple of disadvantages in a parallel (MPI) context.

Since a new class of data analysis codes has come up, with an explicit need for real parallelization, a part of Hypatia has been converted to provide a better tool for those tasks.

In late 2019, first a few handful of Vulcan nodes, then the whole set of 4-core Haswell machines, was reinstalled to create a `Slurm <https://slurm.schedmd.com>`_ cluster. After the main usage (Parallel Bilby) it was called the "Bilby Farm".

The proof of concept was successful, and some Hypatia nodes were converted from HTCondor to Slurm as well. Since these provide 32 cores instead of 4 in a single node, tasks can take better advantage of parallelism, and run on a smaller node number, reducing the risk of hardware failures. The old Vulcan nodes have been disabled now.

**To use the Bilby Farm, login into Hypatia as usual, then ssh to the special headnode vulcan0 (no password etc. required!) where you can use** `Slurm commands <https://slurm.schedmd.com/quickstart.html>`_ **to submit and control your jobs.**

The headnode functionality will be moved to another machine in the near future, during a maintenance period. Updated instructions will be provided.

A `status page <https://hypatia.aei.mpg.de/s/v>`_ is provided. Caveat: There's no auto-update for this status page yet!

Technically, the Bilby Farm is a part of Hypatia, and all shared filesystems are available.

**Caveat:**

The current headnode vulcan0 is at the end of a single optical fibre providing 10 gigabit ethernet — this results in a total bandwidth limit of about 1.2 GB/second. 
