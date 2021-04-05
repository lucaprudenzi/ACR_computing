Archiving Simulation Data
=========================

The /scratch and /work filesystems on Minerva are volatile; i.e. they are not backed up, and users should not trust that data stored there will be available for long periods of time. For example, problems with the filesystem could lead to data loss. Hence, users should archive their important data to ensure it is available in the future.

The Max Planck Society requires that primary data used for publications is securely stored for a period of at least 10 years. See `Long term archiving <https://intranet.aei.mpg.de/general-information/it-department/basic-services/long-term-archiving-langzeitarchivierung>`_.

The Minerva Archive Service makes use of the IBM Tivoli Storage Manager using the dsmc client. Data is transferred to permanent tape storage at Rechenzentrum Garching and FHI Berlin. The institute pays per MB of data stored, and the data is compressed automatically when it is stored on tape. Here we give step-by-step instructions and best-practices for archiving simulation data. All commands should be performed on one of the head nodes, minerva01 or minerva02.

Using Screen
^^^^^^^^^^^^

Since it can take a very long time to archive large amounts of simulation data, and you might want to disconnect your laptop from the network while this is happening, it is recommended to use the Screen program.

Screen allows you to have a permanent session which is not closed if you disconnect from the server. You can use it to run processes which take a long time without worrying about staying logged in to the machine all the time. Enter Screen by typing “screen”. Within Screen you can use normal shell commands. You can give Screen commands by typing CTRL-a followed by a single character (to get the usual CTRL-a behaviour for beginning-of-line, type CTRL-a a). The most important command is CTRL-a d to detach from the Screen session (don't hold down CTRL while pressing the “d”). After detaching, you can log out of the machine and log back in again and resume the session using “screen -r”.

Compressing the data
^^^^^^^^^^^^^^^^^^^^

Go to the directory containing the data you want to archive, for example

.. code-block:: bash

    /scratch/<username>/simulations/mysim

Since transferring data to the archive server take time, it makes sense to compress the data before transferring it. It is also recommended to archive a small number of large files rather than many small files, so we use tar to make a compressed tar archive. In tests, it was significantly faster to first make a gzipped tar file and then archive it than to directly archive the simulation. It also uses less bandwidth. Decide which files you want to exclude from the archive; you can exclude them when creating the tar file.

.. code-block:: bash

    cd simulations
    nice tar cfz mysim.tar.gz --exclude='checkpoint.*.h5' --exclude='*.file_*.h5' mysim

(note that tar is very fussy about the order of the arguments - make sure you put them in the order above). You should adapt the “exclude” parts to your own needs. The “nice” command is used to give the gzip process a low priority to avoid inconveniencing interactive users of the head node.

Archiving the data
^^^^^^^^^^^^^^^^^^

Now you are ready to actually archive the data:

.. code-block:: bash

    dsmc archive <simname>.tar.gz 

The archive will proceed (we have seen transfer speeds between 20 MB/s to 40 MB/s) and indicate progress. At the end, it will print a summary. Check that it reports that it has actually transferred the file. Note that the archive system remembers the path at which the original file was stored on the cluster filesystem.

Listing archived files
^^^^^^^^^^^^^^^^^^^^^^

You can display a list of the files you have archived from the current directory using

.. code-block:: bash

    dsmc query archive '*'

Note that the archive system remembers the directory that the file was archived from, and by default will restore it to the same place (see later). When you do the query command, you have to either be in the right directory, or give the path to the original directory. You can also list all the files archived under a given directory, for example

.. code-block:: bash
    
    dsmc query archive -subdir=yes '/scratch/<username>/*'

You can see files from other users (assuming they have give you permission) using

.. code-block:: bash
    
    dsmc query archive -subdir=yes -fromowner=<username> '/scratch/<username>/*'

Giving access to colleagues

You can enable other users to query and retrieve an archive in the current directory with

.. code-block:: bash
    
    dsmc set access archive <sim>.tar.gz DAMIANA.AEI.MPG.DE <otheruser>

(TODO: update this for Minerva)

Typically, you should routinely give access to your collaborators on a given project so that they can retrieve the data if they need it and you are unavailable.

(TODO: can we give access to groups?)

You can see the permissions you have given other users with

.. code-block:: bash
    
    dsmc query access

You can remove an access rule with

.. code-block:: bash
    
    dsmc delete access

(this is an interactive command - you have to type the number of the rule to delete.)
Deleting the original data

Once the data is archived, the original simulation directory and the tar.gz file can be deleted:

.. code-block:: bash
    
    rm -rf <simname> <simname>.tar.gz

Restoring files from the archive

To restore a file, go into the directory it was archived from and use

.. code-block:: bash
    
    dsmc retrieve <simname>.tar.gz

This will restore it using the original filename. You can now decompress it using

.. code-block:: bash
    
    tar xfz <simname>.tar.gz

Once the file is decompressed, you can delete the tar.gz file:

.. code-block:: bash
    
    rm -f <sim>.tar.gz

You can retrieve a file archived by another user (you need to know who archived the file, and they need to have given you access rights) using:

.. code-block:: bash
    
    dsmc retrieve -fromowner=<otheruser>  /path/to/original/<simname>.tar.gz /path/to/extract/<simname>.tar.gz

Deleting files from the archive
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You may very occasionally want to delete files from the archive (be very careful!). This can be done using the command

.. code-block:: bash
    
    dsmc delete archive '<pathtofile>'

Additional information
^^^^^^^^^^^^^^^^^^^^^^

- It is possible to archive directories rather than files. For example you may wish to make tar files of a number of simulations and archive them all at the same time. You can do this using the -subdir=yes option to dsmc. NB: any directory listed on the dsmc command line should have a trailing “/” character added otherwise dsmc doesn't realise that it is a directory.

- There is additional information about use of the dsmc client at `<http://www.lrz.de/services/compute/backup/>`_, though some of this information might be specific to the LRZ.

- We do not know how to _incrementally_ archive a directory. For example, if you want to archive only what has changed or added since the last time you archived (for example, in an ongoing simulation), there doesn't seem to be any way to do this. *TODO*: ask the support staff of the archive service (again) if this is possible.


