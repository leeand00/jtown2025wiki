# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
    config.vm.provision "shell", inline: "cd /var/www/public && mv ./index.php ./scotchboxinfo.php && wget http://download.dokuwiki.org/out/dokuwiki-5422200921b877a379e34cc4e0fee22a.tgz && tar xvfz dokuwiki-5422200921b877a379e34cc4e0fee22a.tgz"
    config.vm.provision "file", source: "src/000-default.conf", destination: "/tmp/000-default.conf"
    config.vm.provision "shell", inline: "rm -f /etc/apache2/sites-available/000-default.conf && mv /tmp/000-default.conf /etc/apache2/sites-available/000-default.conf && service apache2 stop && service apache2 start"
    config.vm.provision "shell", inline: "cd /tmp && git clone https://github.com/dokufreaks/plugin-pagelist && mv ./plugin-pagelist/ /var/www/public/dokuwiki/lib/plugins/pagelist/"
    config.vm.provision "shell", inline: "cd /tmp && git clone https://github.com/dokufreaks/plugin-tag.git && mv ./plugin-tag/ /var/www/public/dokuwiki/lib/plugins/tag/"
    config.vm.provision "shell", inline: "cd /tmp && git clone https://github.com/splitbrain/dokuwiki-plugin-smtp.git && mv ./dokuwiki-plugin-smtp/ /var/www/public/dokuwiki/lib/plugins/smtp/"
    config.vm.provision "shell", inline: "cd /tmp && git clone https://github.com/splitbrain/dokuwiki-plugin-vshare.git && mv ./dokuwiki-plugin-vshare/ /var/www/public/dokuwiki/lib/plugins/vshare/"
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

end
