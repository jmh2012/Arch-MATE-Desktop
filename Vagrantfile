VAGRANTFILE_API_VERSION = "2"

TEST_MODE = false

PROVIDER_UNDER_TEST = "virtualbox"
NETWORK_PRIVATE_IP_PREFIX = "172.16.3."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.gui = false
    v.memory = 1024
    v.cpus = 1
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # CentOS 7
  config.vm.define "arch" do |arch|
    arch.vm.hostname = "archvm"
    if not TEST_MODE
      arch.vm.box = "archlinux/archlinux"
    else
      arch.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-arch.box"
    end
    arch.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "5"

    # Ansible.
    arch.vm.provision "shell",
      inline: "yes | pacman -S python"
    arch.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.verbose = "v"
    end
    arch.vm.provision :reload
  end
end
