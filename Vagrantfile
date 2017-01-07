unless Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8000
  config.vm.network "forwarded_port", guest: 3306, host: 33060

  config.vm.synced_folder ".", "/usr/src/app", owner: "vagrant", group: "www-data", mount_options: ["dmode=775,fmode=775"]

  config.vm.provision :shell, inline: "apt-get update"
  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: ["/usr/src/app/docker-compose.yml"], rebuild: true, project_name: "wanderlust", run: "always"
end
