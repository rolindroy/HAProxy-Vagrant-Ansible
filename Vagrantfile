VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    base_dir = File.expand_path(File.dirname(__FILE__))
    
    elb_cluster = {
        "elb-server"     => { :ip => "192.168.100.153"},
        "web-server-1"   => { :ip => "192.168.100.161"},
        "web-server-2"   => { :ip => "192.168.100.157"},
    }

    elb_cluster.each_with_index do |(hostname, info), index|
        config.vm.define hostname do |cfg|

          cfg.vm.provider :virtualbox do |vb, override|
            override.vm.network :public_network, ip: "#{info[:ip]}"
            override.vm.hostname = hostname
            vb.name = 'vagrant-' + hostname
          end
        end 
    end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "playbook/playbook.yml"
  end

end
