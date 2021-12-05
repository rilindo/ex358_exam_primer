# Nodes

- ctrl01 - A single control node
- ha01
- ha02
- cache01
- node02
- web01
- web02
- web03
- web04

Required Pre-Tasks

0.  Configure ansible as follows

  - ansible should already be installed.
  - `ansible` user should be created on all nodes
  - directory `exam` should be created under `ansible` home directory on `ctrl01`
  - `ansible` user should able to become root via sudo on `node01` and `ctrl01` without being prompted for the password.
  - `ansible` user should able to login into all nodes without being prompted for the password.

From this point, every playbook and role should be created under `/home/ansible/exam` on `ctrl01`.

1. Create or update inventory file `/home/ansible/exam/inventory.yml` (it should be yaml format) on `ctrl01` and configure `ansible.cfg` to use that inventory. The inventory should contain:

- `web01`, `web02`, `web03`,  and `web03` should be on group `web`
- `node02` should be on group `clients`
- `cache01`, `ha01`, and `ha02` should in group `traffic`
- `ctrl01` should be on group infra (optional)

1. Create playbook `apache2-alt-port.yml` to run again `web01` and `web02` to:

- Install Apache and start it up on boot
- Configure a name-based virtualhost called `earth.example.com` with the document root of `/earth`
- earth.example.com should be configured on port `8888`
- The `/earth` directory should have an index called with the hostname of the server.

2. Create playbook `nginx.yml` to configure `web03` and `web04` to:

- Have nginx be installed and start on boot
- Configure default index page to have the the hostname of the server.

3. Create playbook `squid.yml` to against `cache01`:

- squid be installed and start on boot
- configure to listen on port `8080`
- firewall should be configured to allow access to that port.

4. Create playbook `elinks.yml` to do the following on  `node01`:

- Install `elinks`
- configure elinks environment so that it can browse using `cache01` as the proxy server.

5. Create playbook `ha.yml` to do the following on `ha01`:

- Install and configure haproxy to start up on boot
- Configure haproxy to route traffic to `web03` and `web04` ip addresses

6. Create playbook `ha-ssl.yml` to do the following on `ha02`:

- Install and configure haproxy to start up on boot
- Configure haproxy to route traffic to `web01` and `web02` ip addresses
- Configure SSL termination with haproxy.
