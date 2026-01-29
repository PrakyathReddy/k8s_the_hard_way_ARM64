4 VM's to create using LXD
1. Jumpbox - admin host with 1 cpu, 512MB RAM & 10GB storage
2. Kubernetes server with 1 cpu, 2GB RAM & 20GB storage
3. node-0 as k8s worker node with 1 cpu, 2GB RAM & 20GB storage
4. node-1 as second k8s worker node with 1 cpu, 2GB RAM & 20GB storage

LXC (Linux Containers) allows multiple isolated Linux Systems to run a single host without a hypervisor. LXD manges LXC containers.

$ sudo snap install lxd <br>
$ sudo lxd init <br>
$ lxc launch images:debian/12 jumpbox -c limits.cpu=1 -c limits.memory=512MB <br>
$ lxc launch images:debian/12 server -c limits.cpu=1 -c limits.memory=2GB <br>
$ lxc launch images:debian/12 node-0 -c limits.cpu=1 -c limits.memory=2GB <br>
$ lxc launch images:debian/12 node-1 -c limits.cpu=1 -c limits.memory=2GB <br>
$ lxc config device override server root size=20GB <br>
$ lxc config device override node-0 root size=20GB <br>
$ lxc config device override node-1 root size=20GB <br>

![lxc_list](./images/lxc_list.png)

admin@grid:~/Desktop$ sudo lxc exec jumpbox -- cat /etc/os-release <br>
[sudo] password for admin:  <br>
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)" <br>
NAME="Debian GNU/Linux" <br>
VERSION_ID="12" <br>
VERSION="12 (bookworm)" <br>
VERSION_CODENAME=bookworm <br>
ID=debian <br>
HOME_URL="https://www.debian.org/" <br>
SUPPORT_URL="https://www.debian.org/support" <br>
BUG_REPORT_URL="https://bugs.debian.org/" <br>
