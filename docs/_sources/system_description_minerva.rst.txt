Minerva: High Performance Computing at the AEI
==============================================

Minerva is the HPC cluster of the ACR group. It was delivered by `ClusterVision <https://clustervision.com>`_ and commissioned in 2016.
Purchased for running Numerical Relativity simulations, Minerva replaced `Datura <https://minerva.aei.mpg.de/archive/supercomputers.aei.mpg.de/high-performance-computing/hardware-components>`_.

Minerva ranked 463rd in the `June 2016 TOP500 list <https://www.top500.org/system/178814>`_.

It consists of:

- **594** compute nodes (**dual**-socket, eight core **Intel Haswell** E5-2630v3 (2.40 GHz)
- two login and one management nodes
- two storage systems running `BeeGFS <https://www.beegfs.io/c>`_.
- an `Intel Omni-Path <https://www.intel.com/content/www/us/en/high-performance-computing-fabrics/omni-path-driving-exascale-computing.html>`_ network (**58 GBit/s** bandwidth per node, blocking factor 1.7) 

It provides in total:

- **9504** physical CPU cores
- about **38,000** GB RAM (4 GB per core)
- about **500 TB** of disk space in 10 OSTs RAID-6 (10+2+1)
- a theoretical peak performance of **365 TFlop/s**
- a HPLinPack-measured performance of **302.4 TFlop/s** (83% of peak, parameters: P=22, Q=27, NB=192, N=2020224)

After the upgrade (started Sep 12, finished Dec 20, 2017) it now runs:

- Linux OS: `Debian <https://www.debian.org>`_ 9 (Stretch)
- Interconnect: 10/1 Gigabit Ethernet
- Filesystems: `BeeGFS <https://www.beegfs.io/c>`_ 6.19, `ZFS <https://zfsonlinux.org>`_
- Software: based on `LSC <https://www.ligo.org>`_ `software distribution <http://software.igwn.org>`_
- Job scheduler: `HTCondor <https://research.cs.wisc.edu/htcondor>`_ 8.8.x
- MPI layer: `OpenMPI <https://www.open-mpi.org>`_
- Provisioning: `FAI <https://fai-project.org>`_
- Monitoring: `Ganglia <http://ganglia.info>`_, homegrown 


- Linux OS: CentOS 7.3
- Interconnect: Intel OmniPath 10.5.1.x
- Filesystems: BeeGFS 6.17
- Software: provided by Modules environment
- Job scheduler: Slurm 17.02.7
- MPI layer: Intel MPI from Intel Suite 2016.1 or 2017.4
- Provisioning: TrinityX / Luna
- Monitoring: Zabbix 3.2 
