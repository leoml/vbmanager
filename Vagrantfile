# -*- mode: ruby -*-
# vi: set ft=ruby :

# variaveis

  vhosts =[
    { :hostname => "web", :ip => "127.0.0.1", :fssh_port => "2280", :fweb_port => "8060"},
    { :hostname => "db",  :ip => "127.0.0.1", :fssh_port => "2281", :fweb_port => "8061"},
    { :hostname => "app", :ip => "127.0.0.1", :fssh_port => "2282", :fweb_port => "8062"},
  ]


# inicio

Vagrant.configure("2") do |config|
 
  vhosts.each do |vhost|
    
    config.vm.define vhost[:hostname] do |node|
      node.vm.box = "minimal/trusty64"
      node.vm.hostname = vhost[:hostname]
      node.vm.box_url = "minimal/trusty64"
      node.vm.boot_timeout = 3600

      node.vm.network :forwarded_port, guest:22, host:vhost[:fssh_port], host_ip: vhost[:ip], auto_correct: true
      node.vm.network :forwarded_port, guest:80, host:vhost[:fweb_port], host_ip: vhost[:ip], auto_correct: true
      

      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--name", vhost[:hostname]+"-VG-machine"]
      end
    end
  end

end

