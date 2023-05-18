# Criando o nosso Servidor DNS Master

##  é um comando utilizado no sistema operacional Linux, especialmente nas distribuições baseadas no Debian, como o Ubuntu. Ele é usado para instalar o pacote chamado "bind9", que é a implementação do servidor DNS (Domain Name System) chamada BIND (Berkeley Internet Name Domain). O BIND é uma ferramenta fundamental para a infraestrutura da Internet, pois é responsável pela resolução de nomes de domínio.
```sh
apt install bind9
```

## O arquivo "/etc/hosts" é um arquivo de texto simples que mapeia nomes de host para endereços IP. Ele é usado para resolver nomes de host localmente, antes de consultar um servidor DNS. 
```sh
vim /etc/hosts

127.0.0.1       localhost
127.0.1.1       dns1.empresa.com.br   dns1

172.31.21.152    dns1.empresa.com.br   dns1
```

## O arquivo "/etc/hostname" contém apenas o nome do host do sistema, que é usado para identificar exclusivamente a máquina na rede. Geralmente, esse arquivo contém apenas uma única linha com o nome do host.
```sh
vim /etc/hostname

	dns1.empresa.com.br.
```

## O Netplan é uma ferramenta de configuração de rede introduzida em versões mais recentes do Ubuntu e outras distribuições baseadas no Ubuntu. Ele substitui as configurações tradicionais do arquivo "/etc/network/interfaces" e permite configurar a rede usando um formato YAML mais estruturado.
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

## O diretório "/etc/bind" é o local onde os arquivos de configuração do servidor DNS BIND são armazenados em sistemas Linux, especialmente em distribuições baseadas no Debian, como o Ubuntu. O BIND (Berkeley Internet Name Domain) é uma implementação popular e amplamente usada do servidor DNS.
```sh
cd /etc/bind
ls -l
```

## O arquivo "/etc/bind/named.conf.options" contém as opções de configuração para o servidor DNS BIND. Nesse arquivo, você pode definir várias opções, como as configurações de escuta, encaminhadores (forwarders), restrições de acesso, resolução recursiva, cache DNS e outras opções relacionadas ao comportamento do servidor DNS.
```sh
vim /etc/bind/named.conf.options

listen-on port 53 { 172.31.21.152; };

named-checkconf
```

## O arquivo "named.conf.local" é um arquivo de configuração específico do BIND que contém as zonas de domínio e outras configurações locais do servidor DNS. Nesse arquivo, você pode definir as zonas de domínio que o servidor DNS BIND irá autorizar e servir, bem como outras configurações específicas para cada zona.
```sh
vim named.conf.local

zone "empresa.com.br" {
     type master;
     file "/etc/bind/direta.db";
};
```

## é usado para verificar a sintaxe e a validade da configuração do servidor DNS BIND. Ele é útil para identificar erros de sintaxe ou problemas na configuração antes de reiniciar ou recarregar o serviço do BIND.
```sh
named-checkconf
systemctl status bind9
```







