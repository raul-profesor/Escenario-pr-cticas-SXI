Vagrant.configure("2") do |config|

  N = 3
  (1..N).each do |id|
 
      config.vm.define "servidor#{id}" do |servidor|
        servidor.vm.box = "pow3rline/UbuntuServer21.10"
        servidor.vm.hostname = "raul-server-#{id}"
        servidor.vm.network "public_network", bridge: "enp5s0"
        servidor.vm.provider "virtualbox" do |v|
          v.name = "Server_#{id}"
          #Para poder crear una red interna sin IP inicial asignada
          v.customize ["modifyvm", :id, "--nic3", "intnet"]
          v.customize ["modifyvm", :id, "--intnet3", "Red_privada_1"]
        end
      end
    
      config.vm.define "cliente#{id}" do |cliente|
          cliente.vm.box = "pow3rline/XUbuntu20"
          cliente.vm.hostname = "raul-cliente-#{id}"
        #Le pongo esta IP (antigua red reservada de IBM) aleatoria y que no se usará porque si lo pongo en DHCP
        #luego dhclient tira abajo la configuración de netplan provisionada por ansible
          cliente.vm.network "private_network", ip: "0.0.0.0", auto_network: false,
            virtualbox__intnet: "Red_privada_#{id}"
          cliente.vm.provider "virtualbox" do |v2|
            v2.name = "Cliente_#{id}"
          end
      end
      
      
    if id == N
      config.vm.define "servidor#{id}" do |servidor|
        servidor.vm.box = "pow3rline/UbuntuServer21.10"
        servidor.vm.hostname = "raul-server-#{id}"
        servidor.vm.network "public_network", bridge: "enp5s0"
        servidor.vm.provider "virtualbox" do |v|
          v.name = "Server_#{id}"
          #Para poder crear una red interna sin IP inicial asignada
          v.customize ["modifyvm", :id, "--nic3", "intnet"]
          v.customize ["modifyvm", :id, "--intnet3", "Red_privada_1"]
        end
      end
    
      config.vm.define "cliente#{id}" do |cliente|
          cliente.vm.box = "pow3rline/XUbuntu20"
          cliente.vm.hostname = "raul-cliente-#{id}"
        #Le pongo esta IP (antigua red reservada de IBM) aleatoria y que no se usará porque si lo pongo en DHCP
        #luego dhclient tira abajo la configuración de netplan provisionada por ansible
          cliente.vm.network "private_network", ip: "0.0.0.0", auto_network: false,
            virtualbox__intnet: "Red_privada_1"
          cliente.vm.provider "virtualbox" do |v2|
            v2.name = "Cliente_#{id}"
          end
      end

      config.vm.provision "ansible" do |ansible|
        #ansible.playbook = "ansible/Practica1.yml"
        #ansible.playbook = "ansible/Practica2.1.yml"
        #ansible.playbook = "ansible/Practica2.2.yml"
        #ansible.playbook = "ansible/Practica3.yml"
        #ansible.playbook = "ansible/Practica4.1.2.yml"
        ansible.playbook = "ansible/Practica4.1.3.yml"
        ansible.limit = "all" 
        ansible.groups = {
          "servidores" => ["servidor1", "servidor2", "servidor3"],
          "clientes" => ["cliente1", "cliente2", "cliente3", "servidor3"]
        }
      end
    end
  end
end
