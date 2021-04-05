.. _minerva-policies:

Minerva Policies
================

Definitions
^^^^^^^^^^^

Internal User: Member of the institute who have a valid account provided by the institute's IT department

- External User: Anyone else.
- Host: AEI member responsible for a non-AEI-member (guest, collaborator).
- Director: (of ACR division operating the cluster) `Prof. Alessandra Buonanno <alessandra.buonanno@aei.mpg.de>`_
- Administrator: `directly <steffen.grunewald@aei.mpg.de>`_ or via `HPC support <hpc-support@aei.mpg.de>`_

Overall decision making
^^^^^^^^^^^^^^^^^^^^^^^

- Day-to-day decisions about the running of the cluster are made by the Administrator, if appropriate in discussion with the subscribers of the `minerva-users <http://lists.aei.mpg.de/cgi-bin/mailman/listinfo/minerva-users>`_ mailing list.
- If consensus cannot be reached, the Director has the final say.
- The cluster was bought for numerical relativity, and decisions will be made with that in mind.

Access
^^^^^^

- Accounts may be requested by Internal and External Users - see :ref:`How to get a Minerva account <minerva-account>`.
- Internal Users:
    - All members of the institute may request an account, without getting explicit approval from the Director.
    - Internal User accounts will expire not before the expiry date of the main (institute) account.
- External Users:
    - Accounts for external users must be requested by an AEI Host **and** approved by the Director (i.e. an email confirmation, CC'd to the Administrator). The Host is responsible for the conduct of the collaborator.
    - The host must specify when the account will expire. If desired, a renewal is granted **if approved** by the Director.
- Accounts expire at midnight a.m. UTC on the day provided in the application process,i.e. one cannot access the account starting on this day.
- In the case of any account expiring, the User (and Host, if applicable) are notified at least weekly within the last 60 days of account validity.
- Users must explicitly request account extensions if their contract is renewed.
- Data associated with expired accounts will be removed after **three months** if the account doesn't get reactivated.

Communication with users
^^^^^^^^^^^^^^^^^^^^^^^^

- All cluster Users will be added to the `<minerva-users@aei.mpg.de>`_ mailinglist.
- This list will be used to communicate important information and is used for discussion among users.
- Users are expected to read emails on this list as long as they have an account on the system.
- Internal Users must use their AEI email address.
- External Users must use their official institution email address.

Maintenance
^^^^^^^^^^^

- Scheduled maintenance periods will be announced at least one week in advance. A standard reservation will be made which will prevent jobs that would run into the maintenance window from starting.
- Unscheduled maintenance may be performed without notice at the Administrator's discretion in the following cases:
    - malfunctioning of storage system
    - high probability of data loss
    - high probability of hardware damage
    - severe security problems/holes

Job queues
^^^^^^^^^^

- The cluster supports several queues with different priorities and limits. Generally, numerical relativity jobs are prioritized.
- Jobs are scheduled within queues according to a fair share policy.
- See here for details TODO:FIX

Disk quotas
^^^^^^^^^^^

- Minerva has several different file systems with different quotas.
- The disk quota can be increased by request to the Administrator. If the Administrator considers the request reasonable, it will be implemented. Otherwise, it will be discussed (see Overall Decision Making). TODO:FIX

Users are encouraged to delete or archive old data. Only the home file system is backed up. See here for more details.

Backup/Restore/Archiving
^^^^^^^^^^^^^^^^^^^^^^^^

The AEI has access to a tape archiving system. This should be used for preserving and long-term archiving of data according to the AEI policy on storage of scientific data. The details can be found here.

