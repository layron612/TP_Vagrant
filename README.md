
vagrant fil (première version)
---
```  

Vagrant.configure("2") do |config|

  

  config.vm.box = "generic/rocky9"

  

end
```

vagrant fil (deuxième version)
---
```
Vagrant.configure("2") do |config|

  

  config.vm.box = "generic/rocky9"

  config.vm.network :private_network, ip: "10.1.1.11"

  

  config.vm.hostname = "ezconf.tp1.efrei"

  

  config.vm.disk :disk, name: "Disk_1", size: "20GB"

end
```

vagrant fil (troisième version)
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
