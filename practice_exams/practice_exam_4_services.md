# Nodes

- ctrl01 - A single control node
- db01
- prt01
- mail01
- mail02

Required Pre-Tasks

0.  Configure ansible as follows

  - ansible should already be installed.
  - `ansible` user should be created on all nodes
  - directory `exam` should be created under `ansible` home directory on `ctrl01`
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01` without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- `db01`, `prnt01`, `mail01`,  and `mail02` should be on group `services`
- `ctrl01` should be on group infra (optional)

2. create playbook `printer-queue.yml` to do the following on `prnt01`:

 - Install cups and have it start on boot.
 - Allow access to cups UI from the local network as well as `prnt01`'s ip.
 - configure encryption for CUPS UI.
 - Add generic text-only printer

3. Create playbook `mail.yml` to do the following on `mail01`:

- Configure dovecat client with imap`
- Configure postfix to allow inbound access from within the same network
- Allow inbound access to postfix

4. Create playbook `relay.yml` to do the following on `mail02`:

- Configure mail relay to forward email to `mail01`

5. Create playbook `maria.yml` to do the following on `db01`:

- Install and startup on boot mariadb
- Create database `mydb`
- Create users `mydbadm` to allow access to just `mydb` with the password of `bending`

After this, create the following manually:

- Create table in `mydb` called `mytable` with `first_name` and `last_name` as varchar columns (60 and 120, respectively), with the third column being autoincrement interget `id`.
- Add at least three test records manually with random names.

6. Create playbook `mariadb-backup.yml` to do the following on `db01`:

- Backup `mydb` to file `/opt/mydb.sql`
