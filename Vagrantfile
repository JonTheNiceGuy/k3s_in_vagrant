def gb(gb_size)
  return gb_size*1024
end

k3s_release = "v1.27.2%2Bk3s1"

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.box_check_update = false
  config.vm.network "public_network", use_dhcp_assigned_default_route: true
  config.vm.provider "virtualbox" do |vb|
    vb.memory = gb(4)
    vb.cpus = 2
  end
  config.vm.define "worker1" do |config|
    config.vm.network "private_network", ip: "192.0.2.21"
  end
  config.vm.define "worker2" do |config|
    config.vm.network "private_network", ip: "192.0.2.22"
  end
  config.vm.define "controller" do |config|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = gb(2) # Override for just the controller
    end
    config.vm.network "private_network", ip: "192.0.2.11"
    config.vm.provision :ansible_local do |ansible|
      ansible.playbook          = "ansible/main.yml"
      ansible.install           = true
      ansible.limit             = "all"
      ansible.compatibility_mode = "2.0"
      ansible.host_vars         = {
        "worker1"    => {
          "ansible_host"                 => "192.0.2.21",
          "ansible_user"                 => "vagrant",
          "ansible_ssh_private_key_file" => "/vagrant/.vagrant/machines/worker1/virtualbox/private_key"
        },
        "worker2"    => {
          "ansible_host"                 => "192.0.2.22",
          "ansible_ssh_private_key_file" => "/vagrant/.vagrant/machines/worker2/virtualbox/private_key"
        },
        "controller" => {
          "ansible_connection" => "local"
        }
      }
      ansible.groups            = {
        "workers"      => ["worker1", "worker2"],
        "controllers"  => ["controller"],
        "all:children" => ["workers", "controllers"],
        "workers:vars" => [
          "ansible_user"                  => "vagrant",
          "ansible_ssh_host_key_checking" => "false",
          "ansible_host_key_checking"     => "false"
        ]
      }
    end
  end
end
