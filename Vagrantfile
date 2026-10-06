Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"

  config.vm.define "cliente" do |cliente|
    cliente.vm.hostname = "cliente-parcial"

    cliente.vm.network "private_network",
      ip: "192.168.50.10"

    cliente.vm.provider "virtualbox" do |vb|
      vb.name = "Parcial-Servicios-CLIENTE"
      vb.memory = 2048
      vb.cpus = 2
    end

    cliente.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive

      apt-get update

      apt-get install -y \
        openssh-client \
        openssl \
        ca-certificates \
        curl \
        wget \
        net-tools \
        tcpdump \
        tshark \
        wireshark \
        dnsutils \
        traceroute \
        filezilla \
        git \
        vim \
        nano
    SHELL
  end

  config.vm.define "servidor1" do |srv1|
    srv1.vm.hostname = "srv1-parcial"

    srv1.vm.network "private_network",
      ip: "192.168.50.3"

    srv1.vm.provider "virtualbox" do |vb|
      vb.name = "Parcial-Servicios-SRV1"
      vb.memory = 1024
      vb.cpus = 1
    end

    srv1.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive

      apt-get update

      apt-get install -y \
        ufw \
        iptables \
        iptables-persistent \
        openssh-server \
        openssl \
        ca-certificates \
        curl \
        wget \
        net-tools \
        tcpdump \
        dnsutils \
        traceroute \
        git \
        vim \
        nano

      systemctl enable ssh
      systemctl start ssh

      sysctl -w net.ipv4.ip_forward=1

      grep -q "^net.ipv4.ip_forward=1" /etc/sysctl.conf || \
        echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf

      ufw --force disable
    SHELL
  end

  config.vm.define "servidor2" do |srv2|
    srv2.vm.hostname = "srv2-parcial"

    srv2.vm.network "private_network",
      ip: "192.168.50.2"

    srv2.vm.provider "virtualbox" do |vb|
      vb.name = "Parcial-Servicios-SRV2"
      vb.memory = 1536
      vb.cpus = 1
    end

    srv2.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive

      apt-get update

      apt-get install -y \
        vsftpd \
        openssh-server \
        openssl \
        ca-certificates \
        ufw \
        curl \
        wget \
        net-tools \
        tcpdump \
        dnsutils \
        traceroute \
        git \
        vim \
        nano

      systemctl enable ssh
      systemctl start ssh

      systemctl enable vsftpd
      systemctl stop vsftpd || true

      ufw --force disable
    SHELL
  end

end