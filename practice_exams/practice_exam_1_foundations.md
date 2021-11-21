# Nodes

- ctrl01 - A single control node
- node01
- node02
- node03

Required Pre-Tasks

0.  Configure ansible as follows:

  - ansible should already be installed.
  - `ansible` user should be created on all nodes
  - directory `exam` should be created under `ansible` home directory on `ctrl01`
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01` without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.

Exam tasks

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- group `clients` with `node01`, `node02`, `node03`, and `node04`
- `ctrl01` should be on group infra (optional)

2. Write a play called `install-system-roles.yml` to install Red Hat system roles on `ctrl01`

3. Create a playbook `loop-all-ips.yml` that can print all the ips for each host in the inventory.

4. Create a playbook `nfs-configure.yml` that installs `nfs` service on `node04`, but prevents from starting.

5. Write a playbook `setup-logs.yml`:

 - Configure rsyslog on `node03` to accept logs on port *601*.
 - Allow inbound traffic on port *601* from group `nodes`
 - Configures instances in group `nodes` to send rsyslogs to `node03`

6. Write a playbook `apache-setup.yml` to apply the follow for all instances in group `nodes`:

- Install apache and have it start up automatically.
- Create directory `/www`
- Configure a virtual site called `people.example.com` to listen on port *8888* with the document root pointing to `/www`
- Create an index page call "Hello, People!" in `/www`
- Allow inbound access on port *8888* from the ip of `ctrl01` *only*.
