======
export
======

Exporting a container creates an archive or image that can be sent to a different machine to be imported later. These exported archives can be used as container backups. In this example, 'emby' is the name of the jail:

.. code-block:: shell

  root@nas-mserver: ~# bastille export emby
  Hot exporting 'emby' to a compressed .xz archive.
  Creating temporary ZFS snapshot for export...
  Sending ZFS data stream...
  100 %      659.5 KiB / 9322.1 KiB = 0.071                   0:02             
  Exported '/mnt/storage/bastille/backups/emby_2021-01-08-160136.xz' successfully.

The export sub-command supports both UFS and ZFS storage. ZFS based containers
will use ZFS snapshots. UFS based containers will use `txz` archives.

If the system you are on is using a ZFS file system, a snapshot will be taken immediately while the jail is online and this snapshot is then exported, and deleted.

To ensure a 100% consistent state of jail export, you may use the `-s` flag which will shut down the jail, ZFS snapshot the jail, start the jail, and then export the snapshot, and then delete the snapshot. You can know you are exporting safely because bastille will tell you you are 'Safely exporting, rather than 'Hot exporting' above. In this example, 'emby' is the name of the jail:

.. code-block:: shell

  root@nas-mserver: ~# bastille export emby -s
  Safely exporting 'emby' to a compressed .xz archive.
  [emby]:
  emby: removed

  Creating temporary ZFS snapshot for export...
  [emby]:
  e0a_bastille2
  e0b_bastille2
  emby: created

  Sending ZFS data stream...
  100 %     1342.9 MiB / 3546.4 MiB = 0.379   9.0 MiB/s       6:32             
  Exported '/mnt/storage/bastille/backups/emby_2021-01-08-084413.xz' successfully.
  
  
