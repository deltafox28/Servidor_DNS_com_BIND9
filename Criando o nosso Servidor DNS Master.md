# Criando o nosso Servidor DNS Master

##  é um comando utilizado no sistema operacional Linux, especialmente nas distribuições baseadas no Debian, como o Ubuntu. Ele é usado para instalar o pacote chamado "bind9", que é a implementação do servidor DNS (Domain Name System) chamada BIND (Berkeley Internet Name Domain).
O BIND é uma ferramenta fundamental para a infraestrutura da Internet, pois é responsável pela resolução de nomes de domínio.
```sh
apt install bind9
```

##
```sh
vim /etc/hosts

127.0.0.1       localhost
127.0.1.1       dns1.empresa.com.br   dns1

172.31.21.152    dns1.empresa.com.br   dns1
```

##
```sh
vim /etc/hostname

	dns1.empresa.com.br.
```

##
```sh
vim /etc/netplan/01-netcfg.yaml

search: [empresa.com.br]
```

##
```sh
hostname
hostname -f
hostname -I
```

##
```sh
cd /etc/bind
ls -l
```

##
```sh
vim /etc/bind/named.conf.options

listen-on port 53 { 172.31.21.152; };

named-checkconf
```

##
```sh
vim named.conf.local

zone "empresa.com.br" {
     type master;
     file "/etc/bind/direta.db";
};
```

##
```sh
named-checkconf
systemctl status bind9
```







