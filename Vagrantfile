# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "geerlingguy/centos7"
  config.vm.box_version = "1.2.4"
  config.vm.box_check_update = false

  config.vm.network "forwarded_port", guest: 80, host: 8081
  config.vm.network "forwarded_port", guest: 8080, host: 8082
  config.vm.network "forwarded_port", guest: 8180, host: 8182
  config.vm.network "forwarded_port", guest: 8280, host: 8282
  config.vm.network "forwarded_port", guest: 8380, host: 8382
  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  # If this box will be used on the City of Ottawa network, add some certs to the vm's
  # cert CA store.  This is needed to run git and composer (and probably others)
  config.vm.provision "file", source: "city_certs/CESCA001.pem", destination: "/tmp/CESCA001.pem"
  script = StringIO.new
  script << "update-ca-trust force-enable\n"
  script << "cp -f /tmp/*.pem /etc/pki/ca-trust/source/anchors/\n"
  script << "update-ca-trust extract\n"
  script << "exit 0\n"
  config.vm.provision "shell", inline: script.string  

  
  config.vm.provision "ansible_local", run: "always" do |ansible|
    ansible.version = "latest"
    ansible.limit = "all"
    ansible.raw_arguments = ["--connection=local"]
    ansible.become = true
# Enable the line below if detail logging is reqired
#    ansible.verbose = '-vvv'
    ansible.inventory_path = "provisioning/hosts"
    ansible.playbook = "provisioning/site.yml"
  end
  
 end
