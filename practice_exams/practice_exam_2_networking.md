# Nodes

- ctrl01 - A single control node
- dhcpd01
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
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01` without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`. Note that we will be using `10.0.0.0/24` for ip4 and `2001:DB8::/32` for ipv6

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- group `network` for `net01` and `net02`, and `dhcpd01`
- group `dns` with `ns01`, `ns02`
- `ctrl01` should be on group infra (optional)

2. Create a playbook called `static-assignment.yml` to:

- configure a static ipv4 and ipv6 address for `dhcpd01`. The last ip should end in .10 for both ipv4 and ipv6 addresses

3. Create a playbook called `configure-dhcp01.yml` to run against `dhcpd01`:

- Install dhcpd and radvd for ipv4 and ipv6 address assigned, and enabled on start up.
- Set static ipv4 and ipv6 address for `ns01` and `ns02`
- Configure firewall to allow dhcp assignments

4. Create a playbook called `network-team.yml` to configure a network team on `net01` and `net02`. The IP should end in `.1`  for both ipv4 and ipv6 addresses on `net01` and `.02` for both ipv4 and ipv6 addresses on `net02`

5. Create a playbook called `dns-caching.yml` on `ns02` to:

- Configure dns caching.
- Allow queries from anywhere on the network.

6. Create a playbook called `dns-authoritative.yml` on `ns01` to:

- Configure a forward DNS zone for `example.com` for all nodes within your lab network.
- Configure a reverse DNS zone for `example.com` for all nodes within your lab network.
- Allow queries from anywhere on the network.

Use `/var/named/named.empty` as a base template for creating forward and reverse zones. 
