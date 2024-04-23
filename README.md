
[retour au main](https://github.com/layron612/TP_Vagrant/tree/main)

vagrantfile (première version)
---
```  

Vagrant.configure("2") do |config|

  

  config.vm.box = "generic/rocky9"

  

end
```

vagrantfile (deuxième version)
---
```
Vagrant.configure("2") do |config|

  

  config.vm.box = "generic/rocky9"

  config.vm.network :private_network, ip: "10.1.1.11"

  

  config.vm.hostname = "ezconf.tp1.efrei"

  

  config.vm.disk :disk, name: "Disk_1", size: "20GB"

end
```

vagrantfile (troisième version)
---
```

Vagrant.configure("2") do |config|

  

  config.vm.box = "generic/rocky9"

  config.vm.network :private_network, ip: "10.1.1.11"

  

  config.vm.hostname = "ezconf.tp1.efrei"

  

  config.vm.disk :disk, name: "Disk_1", size: "20GB"

  config.vm.provision "shell", inline: <<-SHELL

    !/bin/bash

    dnf update -y

    apt-get install -y vim python3

  SHELL

end
```

commande de repackaging de rocky-efrei
---
`$ vagrant box repackage rocky-efrei virtualbox 0`

vagrantfile (quatrième version)
---
```
# -*- mode: ruby -*-

# vi: set ft=ruby :

  

Vagrant.configure("2") do |config|

  

  # Definition des machines virtuelles

  nodes = [

    { name: "node1.tp1.efrei", ip: "10.1.1.101", ram: "2048" },

    { name: "node2.tp1.efrei", ip: "10.1.1.102", ram: "1024" }

  ]

  

  # Configuration des machines virtuelles

  nodes.each do |node|

    config.vm.define node[:name] do |node_config|

      node_config.vm.box = "rocky-efrei"  # Remplacez "your-box-name" par le nom de votre box

      node_config.vm.hostname = node[:name] # Nom d'hote de la machine virtuelle

      node_config.vm.network "private_network", ip: node[:ip]  # Adresse IP privee

      node_config.vm.provider "virtualbox" do |vb|

        vb.memory = node[:ram]  # Memoire RAM

        vb.cpus = 1             # Nombre de CPU

      end

    end

  end

  

end
```

ping node2 via node1
---
```
[vagrant@node1 ~]$ ping 10.1.1.102
PING 10.1.1.102 (10.1.1.102) 56(84) bytes of data.
64 bytes from 10.1.1.102: icmp_seq=1 ttl=64 time=1.37 ms
64 bytes from 10.1.1.102: icmp_seq=2 ttl=64 time=2.17 ms
64 bytes from 10.1.1.102: icmp_seq=3 ttl=64 time=2.64 ms
64 bytes from 10.1.1.102: icmp_seq=4 ttl=64 time=1.99 ms
^[64 bytes from 10.1.1.102: icmp_seq=5 ttl=64 time=1.56 ms
64 bytes from 10.1.1.102: icmp_seq=6 ttl=64 time=2.11 ms
64 bytes from 10.1.1.102: icmp_seq=7 ttl=64 time=2.54 ms
64 bytes from 10.1.1.102: icmp_seq=8 ttl=64 time=1.85 ms
64 bytes from 10.1.1.102: icmp_seq=9 ttl=64 time=3.04 ms

^C
--- 10.1.1.102 ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 8022ms
rtt min/avg/max/mdev = 1.371/2.141/3.037/0.500 ms
[vagrant@node1 ~]$
```

[retour au main](https://github.com/layron612/TP_Vagrant/tree/main)
