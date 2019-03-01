# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/alpine38"

  config.vm.provision "shell", inline: <<-SHELL
echo "vagrant.$(ip a show dev eth0 | grep -m1 inet | awk '{print $2}' | cut -d'/' -f1).xip.io" > /etc/hostname
hostname -F /etc/hostname
echo "cgroup /sys/fs/cgroup cgroup defaults 0 0" >> /etc/fstab
mount /sys/fs/cgroup
echo "Downloading k3s..."
wget https://github.com/rancher/k3s/releases/download/v0.1.0/k3s -O /usr/sbin/k3s --quiet
chmod +x /usr/sbin/k3s
cat<<EOF>/etc/init.d/k3s
#!/sbin/openrc-run

name="K3S"
command="/usr/sbin/k3s"
command_args="server"
command_background="yes"
command_user="root"
pidfile="/run/k3s/k3s.pid"
start_stop_daemon_args="--make-pidfile -2 /var/log/k3s/server.log"

depend() {
        need net
}

start_pre() {
        checkpath --directory --owner root:root --mode 0775 /run/k3s /var/log/k3s
}
EOF
chmod +x /etc/init.d/k3s
rc-update add k3s default
service k3s start
echo "alias kubectl='sudo k3s kubectl'" >> /etc/profile
  SHELL
end
