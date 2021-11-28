# Nodes

- ctrl01 - A single control node
- node04
- san01
- nfs01
- smb01

Required Pre-Tasks

0.  Configure ansible as follows

  - ansible should already be installed.
  - `ansible` user should be created on all nodes
  - directory `exam` should be created under `ansible` home directory on `ctrl01`
  - `ansible` user should able to become root via sudo on `node04` and `ctrl01` without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.


1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- `san01`, `nfs01`, and `smb01` should be on group `storage`
- `node03` should be on group `clients`
- `ctrl01` should be on group infra (optional)

2. Create a playbook called `nfs-server.yml` to run against `nfs01`. It will:
- Create a directory `/shared_nfs` generate a file `text.txt` with the word `word`.
- Install and configure NFS server. The NFS server should start up at boot.
- Allow access from `node04`

3. Create a playbook called `nfs-client.yml` to run against `node04`. It will.

- Mount `/export` on `nfs01` on `/mnt/nfs`

4. Create a playbook called `iscsi-target.yml` to configure the following on `san01`:

- Setup iscsi service and have start from boot.
- Create a `100` MiG target.
- Allow access to service from `node04`.

5. Create a playbook called `iscsi-client.yml` to configure the following on `node04`:

- Configure iscsi client against `san01`
- Create a volume group `iscsi_vg` using the entire iscsi disk that is created.
- Create a volume group `iscsi_lv` using the entire volume group `iscsi_vg`.
- Format the file system on `iscsi_lv` with nfs and mount it on `/mnt/iscsi`.

6. Create a playbook called `smb-server.yml` to configure the following on `smb01`:

- Create local and samba users `jiro`, `han`, `mary`, and `chen` in a group `knights`
- Create directory `earth` and create a file `bend.txt` with the words `avatar knights`.
- Create samba share called `earth` and allow access to the above users and allow access from `node04`

7. Create a playbook called `smb-client.yml` to configure the following on `node04`:

- Setup a multi-user samba mount for `earth` on `smb0` using `chen` as the user.
- Mount volume on `/mnt/bend`
