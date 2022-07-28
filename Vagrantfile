#Definição de maquinas do Laboratório do Elastic Stack
machines = {
	"node-master"       => { "ip" => "10",  "memory" => "3072", "cpus" => "2" },
	"node-data"     => { "ip" => "11",  "memory" => "3072", "cpus" => "2" },
        "monitoring"         => { "ip" => "20", "memory" => "2048", "cpus" => "1" },
}

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  machines.each do |name,conf|
    config.vm.define "#{name}" do |srv|
      srv.vm.hostname = "#{name}"
      srv.vm.network 'private_network', ip: "192.168.63.#{conf["ip"]}"
      srv.vm.provider 'virtualbox' do |vb|
        vb.memory = "#{conf["memory"]}"
        vb.cpus = "#{conf["cpus"]}"
        vb.customize ["modifyvm", :id, "--groups", "/ElasticStack"]
      end
      
      srv.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "provision/elastic_stack_provision.yaml"
        ansible.become = true
      end

    end
  end

end
