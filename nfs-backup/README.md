# nfs-backup

This is automation for backing up my homelab's NAS to BorgBase.

Assumptions:

- An NFS share (currently assumes just one) to back up
- The use of BorgBase, or at least Borg, and an _already initialized_
  repository.
- The use of OpenShift

It uses Kustomize and does the following:

- Creates a PV that points to the NFS server and is tied to a specific PVC
  - You are expected to edit it to point to your own NFS server and volume
- Creates a PVC that gets immediately bound to the above PV
- Creates a secrets for the ssh key and `borgmatic.yml` config
  - You are expected to generate an ssh key and move it to `ssh_private_key.txt`
  - You are expected to move `borgmatic.yml.example` to `borgmatic.yml` and
    edit it as you see fit.
- Creates a CronJob that uses all of the above and creates archives in the
  repository.
