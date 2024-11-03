# ansible-stuff

Some Ansible playbooks I'm using.

Topics:

- [backup](backup/): some backup stuff, restic, vzdump (Proxmox)
- [tasmota-delock](tasmota-delock/): firmware version / updates


## migrate-lxc-proxmox-through-backup.yml

Stop LXC container on host A, run backup to Proxmox backup server,
run restore from Proxmox backup server on host B,
start LXC container on host B.

Remove LXC container manually on host A when everything's fine.


## proxmox-start-all-lxcs.yml

Start all LXCs on the specified target Proxmox host
