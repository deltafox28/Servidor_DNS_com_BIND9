# Criando a nossa Zona Direta

##
```sh
vim /etc/bind/direta.db

; IN é internet
; Arquivo que representa a zona de "empresa.com.br"
;
$TTL 8h ;
@       IN      SOA     dns1.empresa.com.br. root.empresa.com.br. (
                        2017071101 ; serial
                        3h ; refresh
                        30m ; retry
                        4d ; expiry
                        1h ; negative cache
);
@       IN      NS      dns1.empresa.com.br.
@       IN      NS      dns2.empresa.com.br.
@       IN      MX      5 mail.empresa.com.br.
dns1    IN      A       192.168.88.2
dns2    IN      A       192.168.88.3
samba   IN      A       192.168.88.5
dhcp    IN      A       192.168.88.4
www     IN      A       192.168.88.7
web     IN      CNAME   www
ftp     IN      CNAME   www
firewall IN     A       192.168.88.1
proxy   IN      CNAME   firewall
mail    IN      A       192.168.88.3
smtp    IN      CNAME   mail
imap    IN      CNAME   mail
pop3    IN      CNAME   mail
```


##
```sh
named-checkzone empresa.com.br /etc/bind/direta.db
```

##
```sh
dig -t soa empresa.com.br
```













