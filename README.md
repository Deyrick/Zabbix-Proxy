# Instalando Zabbix Proxy on CentOS/RHEL


### Definir timezone

```shell

timedatectl set-timezone America/Sao_Paulo

```

### Configure o chrony (NTP) para corrigir data e hora


```shell

dnf -y install chrony

```
```shell

systemctl enable --now chronyd

```


### Instalar utilitários

```shell

dnf install -y net-tools vim nano epel-release wget curl tcpdump

```

### Instalar o pacote do mysql server

```shell

dnf -y install mysql-server

```

### Habilitar e iniciar serviço do MySQL

```shell

ssystemctl enable --now mysqld

```


### Instalando o Repositório da Zabbix

```
rpm -Uvh https://repo.zabbix.com/zabbix/6.0/rhel/9/x86_64/zabbix-release-6.0-4.el9.noarch.rpm
  
 ```
 ```
dnf clean all 
  
 ```
 
  ### Instalando o Proxy:
  
  
  ```
  # dnf install zabbix-proxy-mysql zabbix-sql-scripts zabbix-selinux-policy 
   
```

### Criar a database


```shell

mysql -uroot -p

```
Ps: se você não criou uma senha e só dar um enter

### dentro do Mysql


```shell 
create database zabbix_proxy character set utf8mb4 collate utf8mb4_bin;

create user zabbix@localhost identified by 'password';

grant all privileges on zabbix_proxy.* to zabbix@localhost;

quit; 

```
Ps no campo 'password', coloque a senha que seu "coração manda "

###  Carregando as tabelas necessárias para funcionar

```shell

scat /usr/share/zabbix-sql-scripts/mysql/proxy.sql | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix_proxy

```

###  Usando seu editor de texto favorito edite o arquivo de configuração 

```shell
vi /etc/zabbix/zabbix_proxy.conf

nano /etc/zabbix/zabbix_proxy.conf

vim /etc/zabbix/zabbix_proxy.conf									
	
```												
Ps: Pessoal que usa o "vim", vocês usam todas  as funcionalidades mesmo ou e modinha?											

###  Dentro do arquivo altere o parâmetro abaixo com a sua senha: 
```shell
 DBPassword=password 
```
###  Habilitando o  Serviço e configurando para iniciar apos o reboot do servidor:
```shell
 systemctl restart zabbix-proxy
```

```shell
 systemctl enable zabbix-proxy
```

Ps caso as coisas não funcionem como você esperava, obtenha alguma mensagem de erro quando iniciar, use o comando abaixo para analisar o problema:

```shell
 tail -f /var/log/zabbix/zabbix_proxy.log
```

Obrigado por te chegado até aqui. 


<p align="center">
<img src="https://github.com/Deyrick/Fedora/blob/main/2021-09-12_16-57.png" >
</p>

