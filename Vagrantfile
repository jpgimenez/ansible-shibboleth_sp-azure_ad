# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "test", primary: true, autostart: true do |test|
    test.vm.box = "ubuntu/xenial64"

    test.vm.network "forwarded_port", guest: 80, host: 9080
    test.vm.network "forwarded_port", guest: 443, host: 9081
    test.vm.network "forwarded_port", guest: 8080, host: 9082

    test.vm.provision "ansible" do |ansible|
      ansible.playbook = "test.yml"
      ansible.host_vars = {
        "test" => {"ansible_python_interpreter" => "/usr/bin/python3"
                  },
      }
    end
  end

  config.vm.define "fedora", primary: false, autostart: false do |fedora|
    fedora.vm.box = "fedora/27-cloud-base"

    fedora.vm.network "forwarded_port", guest: 80, host: 9080
    fedora.vm.network "forwarded_port", guest: 443, host: 9081
    fedora.vm.network "forwarded_port", guest: 8080, host: 9082

    fedora.vm.provision "ansible" do |ansible|
      ansible.playbook = "test.yml"
      ansible.host_vars = {
        "fedora" => {"ansible_python_interpreter" => "/usr/bin/python2"
                    },
      }
    end
  end

  config.vm.define "centos7", primary: false, autostart: false do |centos7|
    centos7.vm.box = "centos/7"

    centos7.vm.network "forwarded_port", guest: 80, host: 9080
    centos7.vm.network "forwarded_port", guest: 443, host: 9081
    centos7.vm.network "forwarded_port", guest: 8080, host: 9082

    centos7.vm.provision "ansible" do |ansible|
      ansible.playbook = "test.yml"
    end
  end

end
