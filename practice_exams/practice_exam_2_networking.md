# Nodes

- ctrl01 - A single control node
- dhcp01
- net01
- net02
- ns01
- ns02

(note: net01 and net02 should have dual nics)

Required Pre-Tasks

0.  Configure ansible as follows

  - ansible should already be installed.
  - `ansible` user should be created on all nodes
  - directory `exam` should be created under `ansible` home directory on `ctrl01`
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01 without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- group `network` for `net01` and `net02`, and `dhcp01`
- group `routing` with `ns01`, `ns02`
- `ctrl01` should be on group infra (optional)


2. Create a playbook called `configure-dhcp01.yml` to:

- Install dhcpd and radvd for ipv4 and ipv6 address assigned, and enabled on start up.
- Set static ipv4 and ipv6 address for `ns01`
- Configure firewall to allow dhcp assignments

Use `192.168.2.0/24` for ip4 and `2001:DB8::/32` for ipv6

3. Create a playbook called `static-assignment.yml` to:

- configure a static ipv4 and ipv6 address for `net02`. The last ip should end in .2  both ipv4 and ipv6 addresses

4. Create a playbook called `network-team.yml` to configure a network team on `net01`. The IP should end in .1 for both ipv4 and ipv6 addresses.

5. Create a playbook called `dns-caching.yml` on `ns02` to:

- Configure dns caching.
- Allow queries from anywhere on the network.

6. Create a playbook called `dns-authoriative.yml` on `ns02` to:

- Configure an forward DNS zone for `example.com`.
- A reverse dns zone for the 192.168.2.0 network.
- All nodes except for `ctrl01` should have forward and reverse dns entries.
- Allow queries from anywhere on the network.
