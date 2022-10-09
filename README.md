# Install Zabbix Proxy on CentOS/RHEL


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


### Instalando o Repositorio da Zabbix

```
rpm -Uvh https://repo.zabbix.com/zabbix/6.0/rhel/9/x86_64/zabbix-release-6.0-4.el9.noarch.rpm
  
 ```
 ```
dnf clean all 
  
 ```
 
  ### Optionally, enable the Nonfree repository:
  
  
  ```
  sudo dnf install \
  https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

   sudo dnf group update core
   
```

### Multimedia Codecs

The basics that work

```shell

sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel

sudo dnf install lame\* --exclude=lame-devel

sudo dnf group upgrade --with-optional Multimedia


```

### For OpenH264 in Firefox I run:


```shell 

sudo dnf -y config-manager --set-enabled fedora-cisco-openh264

sudo dnf -y install gstreamer1-plugin-openh264 mozilla-openh264


```
### Install Edge "Optional"

```shell

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc -y

sudo dnf -y config-manager --add-repo https://packages.microsoft.com/yumrepos/edge

sudo mv /etc/yum.repos.d/packages.microsoft.com_yumrepos_edge.repo /etc/yum.repos.d/microsoft-edge-dev.repo 

sudo dnf -y install microsoft-edge-dev

```


### Delete Firefox "Optional"

```shell

sudo dnf -y remove firefox*

sudo dnf clean all

```
Afterwards you need to open Firefox, go to menu → Add-ons → Plugins and enable OpenH264 plugin. You can do a simple test whether your H.264 works in RTC on this page (check Require H.264 video).

### Optional: "Software that you will need sometime"

1. Qbittorrent
2. Neofectch

```shell

sudo dnf -y install qbittorrent 

sudo dnf -y install neofetch

```

### Firefox

### Optional: Force GPU rendering to smooth out page scrolling

Firefox in Gnome can experience screen tearing and other performance-inhibiting behavior. This may be adjustable by forcing GPU rendering, though it may impact power usage and stability. This has only been tested using NVIDIA GPUs.


1. Navigate to`about:config` in the Firefox URL bar
2. Select Accept the Risk and Continue
3. Copy and paste`layers.acceleration.force-enabled` into the search box and Enable it
4. Copy and paste`layers.force-active` into the search box and Enable it
5. Restart Firefox and observe smoother scrolling behavior




<p align="center">
<img src="https://github.com/Deyrick/Fedora/blob/main/2021-09-12_16-57.png" >
</p>
