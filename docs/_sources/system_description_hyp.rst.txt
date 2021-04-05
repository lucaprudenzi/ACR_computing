Hypatia: High Throughput Computing at the AEI
=============================================

Hypatia is the new HTC cluster of the Astrophysical and Cosmological Relativity (ACR) group of the `a Max Planck Institute for Gravitational Physics (Albert Einstein Institute) <https://www.aei.mpg.de/>`_.

It was delivered by `a Tradex Systems <http://www.tradex.pl>`_, and after successfully passing three test stages, it was finally commissioned in spring 2019.

Purchased for running GW detector data analysis and simulations, Hypatia replaces Vulcan.

After complete installation by Tradex Systems, it now consists of:

- **262** GIGABYTE compute nodes (dual-socket, sixteen-core, SMT-enabled **AMD EPYC (Naples)** 7351 (2.40 GHz), of which **14** provide 8 GB RAM per core (4 GB per core otherwise)
- two login nodes (using identical hardware)
- two commodity HUAWEI ethernet networks (for data and management) 

to which we added:

- a management and setup server (**arm64** architecture, `a ThunderX based <http://www.tradex.pl/>`_)
- a 300 TB **/work** storage system, running BeeGFS, provided by `a MEGWARE <https://www.megware.com>`_
- two 70 TB file servers (for **/home** etc.), based on ZFS, also from `a MEGWARE <https://www.megware.com>`_ 

It provides in total:

- **8384** physical CPU cores
- about **34,500 GB** RAM (4 GB per core)
- about **400 TB** of disk space 

It is running:

- Linux OS: `Debian <https://www.debian.org>`_ 9 (Stretch)
- Interconnect: 10/1 Gigabit Ethernet
- Filesystems: `BeeGFS <https://www.beegfs.io/c>`_ 6.19, `ZFS <https://zfsonlinux.org>`_
- Software: based on `LSC <https://www.ligo.org>`_ `software distribution <http://software.igwn.org>`_
- Job scheduler: `HTCondor <https://research.cs.wisc.edu/htcondor>`_ 8.8.x
- MPI layer: `OpenMPI <https://www.open-mpi.org>`_
- Provisioning: `FAI <https://fai-project.org>`_
- Monitoring: `Ganglia <http://ganglia.info>`_, homegrown 

We had `integrated Vulcan <https://hypatia.aei.mpg.de/cgi-bin/hypatia-index.cgi?p=vulcannodes#main>`_ nodes into this setup, for "slim" jobs (up to 4–6 physical cores) although they are currently switched off. 
