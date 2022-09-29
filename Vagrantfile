Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
   vb.memory = 1024
 end



    config.vm.define "wordpress" do |m|
       # m.vm.box = "ubuntu/trusty64"
       m.vm.provider "virtualbox" do |v|
          v.memory = 1024
       end
      m.vm.network "private_network", ip: "172.17.177.40"
      m.vm.provision "shell",
           inline: "cat /vagrant/configs/id_bionic.pub >> .ssh/authorized_keys"
    end


    config.vm.define "ansible" do |ansible|
       ansible.vm.provider "virtualbox" do |vb|
            vb.memory = 1024
            vb.cpus = 2
            vb.name = "Ansible"
        end
        ansible.vm.network "private_network", ip: "172.17.177.39"
        ansible.vm.provision "shell",
             inline: "cp /vagrant/id_bionic  /home/vagrant && \
                     chmod 600 /home/vagrant/id_bionic && \
                     chown vagrant:vagrant id_bionic"
        ansible.vm.provision "shell",
            inline: "apt-get update && \
                     apt-get install -y software-properties-common && \
                     apt-add-repository --yes --update ppa:ansible/ansible && \
                     apt-get install -y ansible"

         ansible.vm.provision "shell",
             inline: "cp /vagrant/configs/ansible/hosts  /home/vagrant && \
                      chmod 600 /home/vagrant/hosts && \
                      chown vagrant:vagrant hosts && \
                      cat /home/vagrant/hosts >> /etc/ansible/hosts "
       # ansible.vm.provision "shell",
       #      inline: "ansible-playbook -i /vagrant/configs/ansible/hosts"
    end

end
