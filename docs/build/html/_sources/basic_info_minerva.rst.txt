.. _basic-info:

Basic information
=================

Queues
^^^^^^

The cluster has the following queues:

.. list-table::
    :header-rows: 1
    :stub-columns: 1

    * - Queue
      - Description
    * - devel
      - | Accessible by all users. Used for interactive and debugging use,
        | short duration only. Initially 16 separate nodes.
    * - urgent
      - | NR users may submit to this queue if they feel their job is more urgent
        | than some other NR jobs. They should be prepared to justify (if asked)
        | on the mailing list, or to the Director, why the jobs are urgent.
        | Non-NR users should ask on the mailing list first if there are objections 
        | to running in this queue, and say how much they expect to use and for
        | how long. If consensus cannot be reached, the Director decides.
    * - nr
      - Only for NR users
    * - normal
      - Accessible by all users
    * - fillin
      - | Accessible by all users. Can run longer jobs but they may be 
        | preempted (killed) by jobs in higher priority queues. See Preemption.

Additional information:
 
    - There is no maximum walltime for jobs in **fillin**.
    - The maximum walltime of a job in **devel** is 8 hours.
    - The maximum walltime of a single job is 24 hours in all other queues.
    - The order of priority of queues is devel > urgent > nr > normal > fillin. A job in a lower priority queue will not be started if it would delay the start of a job in a higher priority queue.

Disk quotas
^^^^^^^^^^^

Minerva provides three separate filesystems. Initial disk quotas are:


.. list-table::
    :header-rows: 1
    :stub-columns: 1
    
    * - FS
      - Total size
      - Disk quota
      - Inode **(*)** file limit

    * - /home
      - 45 TB
      - 10 GB
      - 1 Million
    * - /work
      - 90 TB
      - 100 GB
      - 4 Million
    * - /scratch
      - 320 TB 
      - None (\**)
      - None (\**)

(\*) directories count 3-fold; (\**) provided disk space is available.

On /scratch, users are encouraged to delete or archive old data, either to /work or to Archive Storage. /scratch is not automatically purged, however users having data older than 3 months may get reminders to clean up.

Note: **Only the home file system is backed up**

Backup and archiving
^^^^^^^^^^^^^^^^^^^^

- /home is backed up nightly
- Other filesystems are not backed up
- Restoration of files currently requires asking the Administrator, but in future will be possible independently
- Files will be available for restore from the backup up to 90 days after their deletion.
- Directories (**nobackup, NOBACKUP, NoBackup, scratch, SCRATCH, .cache**) and files (***.swp** and **core.[0-9][0-9]***) are excluded from backup
- ``/scratch`` and ``/work`` should be considered volatile systems; data is not backed up, and is at risk of filesystem crashes. The AEI has access to a tape archiving system. This should be used for preserving and long-term archiving of data according to the AEI policy on `storage of scientific data <https://intranet.aei.mpg.de/general-information/it-department/basic-services/long-term-archiving-langzeitarchivierung>`_
