Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.box_check_update = false

  hosts = {
    "cyril" => "192.168.121.10",
    "node1" => "192.168.121.11",
    "node2" => "192.168.121.12",
    "node3" => "192.168.121.13"
  }

  hosts.each do |name, ip|
    config.vm.define name do |vm|
      vm.vm.hostname = name
      vm.vm.network "private_network", ip: ip, libvirt__network_name: "vagrant-libvirt", type: "static"

      vm.vm.provider :libvirt do |libvirt|
        libvirt.memory = 1024
        libvirt.cpus = 1
      end

      vm.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install -y openssh-server sudo
        systemctl enable ssh
        systemctl start ssh
        echo "# ---Other Vagrant provisioned hosts---" >> /etc/hosts
      SHELL

      hosts.each do |other_name, other_ip|
        next if name == other_name
        vm.vm.provision "shell", inline: "echo '#{other_ip} #{other_name}' >> /etc/hosts"
      end

      vm.vm.provision "shell", inline: "echo '# ---End of other Vagrant hosts---' >> /etc/hosts"

      if name == "cyril"
        vm.vm.provision "shell", inline: <<-SHELL
          apt install -y ansible
          useradd -m -s /bin/bash cansible
          echo "cansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/cansible
          chmod 0440 /etc/sudoers.d/cansible
          mkdir -p /home/cansible/.ssh
          chown -R cansible:cansible /home/cansible/.ssh
        SHELL
      end

      if ["node1", "node2", "node3"].include?(name)
        vm.vm.provision "shell", inline: <<-SHELL
          useradd -m -s /bin/bash management
          echo "management ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/management
          chmod 0440 /etc/sudoers.d/management
          mkdir -p /home/management/.ssh
          chown -R management:management /home/management/.ssh
        SHELL
      end
    end
  end
end

