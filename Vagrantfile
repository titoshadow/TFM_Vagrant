Vagrant.configure("2") do |config|
    config.vm.box = "almalinux/8"
    config.vm.define "mvp"
    config.vm.hostname = "dev.tfm.com"

    config.vm.network "public_network", type: "dhcp"
    config.vm.network "forwarded_port", guest: 80, host: 8080 # Web
    config.vm.network "forwarded_port", guest: 1883, host: 1883 # MQTT
    config.vm.network "forwarded_port", guest: 8883, host: 8883 # MQTT SSL
    config.vm.network "forwarded_port", guest: 8081, host: 8081 # API HTTP 
    config.vm.network "forwarded_port", guest: 8083, host: 8083 # MQTT Websocket SSL
    config.vm.network "forwarded_port", guest: 8084, host: 8084 # MQTT Websocket
    config.vm.network "forwarded_port", guest: 18083, host: 18083 # Dashboard

    config.vm.provider "virtualbox" do |v|
        v.name = "TFM"
        
        if Vagrant.has_plugin?("vagrant-vbguest") then
            config.vbguest.auto_update = false
        else
            v.check_guest_additions = false
        end
    end

    config.vm.provision "shell", path: "provision.sh"
end