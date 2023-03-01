# Backup stuff

I have 2 backup servers in my environment: backup4.lan and backup5.lan. The backup storage is mounted as /media/backup1. It's a brfs volume. Subvolumes are created for each host.

## run-restic-backup.yml

The main part. I'm using this playbook to do backups.

`ansible-playbook playbooks/run-restic-backup.yml --extra-vars "target=backup*.lan,testct*.lan,put-your-hostname-here"`

There's a subtask which is executed by the playbook. 
MQTT messages are sent when the backup is started, and after the backup has finished.

I've removed some (private) parts of the backup script.

## prepare-restic-backup-client.yml

When I create new Linux containers, or VMs, I ran this playbook to setup the backup partitions and exchange the public SSH keys.
