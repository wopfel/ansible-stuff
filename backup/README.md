# Backup stuff

## Restic

I have 2 backup servers in my environment: backup4.lan and backup5.lan. The backup storage is mounted as /media/backup1. It's a brfs volume. Subvolumes are created for each host.

### run-restic-backup.yml

The main part. I'm using this playbook to do backups.

`ansible-playbook playbooks/run-restic-backup.yml --extra-vars "target=backup*.lan,testct*.lan,put-your-hostname-here"`

There's a subtask which is executed by the playbook. 
MQTT messages are sent when the backup is started, and after the backup has finished.

I've removed some (private) parts of the backup script.

### prepare-restic-backup-client.yml

When I create new Linux containers, or VMs, I ran this playbook to setup the backup partitions and exchange the public SSH keys.


## Proxmox VE backup / vzdump

I have a separate server where proxmox backup is installed. Running vzdump, a dump of each Linux container, and VM can be created and stored on the PBS.

### start-proxmox-backup-server.yml

This will wake my backup server, and mount the encrypted partition where the backups are stored.

After the server is up, I start `vzdump-one-by-one-proxmox.yml`.

### vzdump-one-by-one-proxmox.yml

The playbook fetches all IDs from both proxmox VE servers (proxmox3, and proxmox4 in my environment).

Start the backup by running `ansible-playbook vzdump-one-by-one-proxmox.yml --extra-vars "bkpserver=backup7.lan"`.


## Borg

Old files. Put in separate folder. Not used anymore.