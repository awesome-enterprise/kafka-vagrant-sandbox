ENV["LC_ALL"] = "en_US.UTF-8"

# if sth. gets changed here, also adapt /ansible/inventories/vbox/hosts
ZOOKEEPER = 3
KAFKA = 3

ZOOKEEPER_MEMORY = "512";
KAFKA_MEMORY = "1024";

ZOOKEEPER_SUBNET = "192.168.10.1"
KAFKA_SUBNET = "192.168.11.1"

Vagrant.configure("2") do |config|

    required_plugins = %w( vagrant-hostsupdater )
    required_plugins.each do |plugin|
        system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
    end

    config.vm.box = "ubuntu/focal64"
        if Vagrant.has_plugin?("vagrant-vbguest") then
            config.vbguest.auto_update = false
        end
    config.vm.box_check_update = true

    config.vm.synced_folder "ansible", "/home/vagrant/ansible", create: true

    (1..ZOOKEEPER).each do |i|
        config.vm.define "zookeeper#{i}" do |zookeeper|
            zookeeper.vm.hostname = "zookeeper#{i}"
            zookeeper.vm.provider "zookeeper" do |vb|
                vb.memory = ZOOKEEPER_MEMORY
                vb.cpus = "1"
            end
            zookeeper.vm.network :private_network, ip: "#{ZOOKEEPER_SUBNET}#{i}", auto_config: true

            id_rsa_pub = File.read("./shared-keys/ssh_key.pub")
            config.vm.provision "copy ssh public key", type: "shell",
              inline: "echo \"#{id_rsa_pub}\" >> /home/vagrant/.ssh/authorized_keys"
        end
    end

    (1..KAFKA).each do |i|
        config.vm.define "kafka#{i}" do |kafka|
            kafka.vm.hostname = "kafka#{i}"
            kafka.vm.provider "virtualbox" do |vb|
                vb.memory = KAFKA_MEMORY
                vb.cpus = "1"
            end
            kafka.vm.network :private_network, ip: "#{KAFKA_SUBNET}#{i}", auto_config: true

            id_rsa_pub = File.read("./shared-keys/ssh_key.pub")
            config.vm.provision "copy ssh public key", type: "shell",
              inline: "echo \"#{id_rsa_pub}\" >> /home/vagrant/.ssh/authorized_keys"
        end
    end
end
