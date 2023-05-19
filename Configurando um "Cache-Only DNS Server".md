# Configurando um "Cache-Only DNS Server"

##
```sh
yum install unbound bind-utils
```

##
```sh
sed -i '/interface: 0.0.0.0$/s/#//' /etc/unbound/unbound.conf
sed -i 's/127.0.0.0\/8 allow/192.168.0.0\/24 allow/' /etc/unbound/unbound.conf
```

##
```sh
unbound-control-setup 
unbound-checkconf
systemctl enable unbound
```

##
```sh
service unbound start
```

##
```sh
service unbound status
```

##
```sh
firewall-cmd --permanent --add-service dns
firewall-cmd --reload
```

##
```sh
dig @localhost example.com
dig +dnssec DNSKEY rhatcert.com
```














