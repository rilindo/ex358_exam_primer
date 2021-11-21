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
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01 without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- `db01`, `prt01`, `mail01`,  and `mail02` should be on group `services`
- `ctrl01` should be on group infra (optional)

2. On `ns01`:

  - Configured authoritative DNS server with forward and reverse DNS for all the listed nodes using `/var/named/named.empty`

3. On `ns02`:

  - Configure caching server that forward requests over to ns01

4. On `prt01`:

 - Install and configure printer with queue.

5. On 'mail01':

- Configure dovecat client with imap`
- Configure postfix to allow inbound access from within the same network
- Allow inbound access to postfix

6. On `mail02`:

- Configure mail relay to forward email to mail02

7. On `db01`:

- Install and startup on boot mariadb
- Create database `mydb`
- Create users `mydbadm` to allow access to just `mydb`
- Create table in `mydb` called `mytable` with `first_name` and `last_name` as the columns. Add several records
- Backup `mydb` to file `/opt/mydb.sql`