## <span style="color: #3594FF">Configuração Básica de Switches<span>
### 1- Configurar os nomes para os <span style="color: #3594FF">switches</span>:


```
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1-Zg
SW1-Zg(config)#
```

(fazer o mesmo para os restantes switches)

### 2- Configurar Passwords para os <span style="color: #3594FF">switches</span>
#### 2.1- Configurar User EXEC Password
```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# line console 0
SW1-Zg(config-line)# password cisco  #especifica a password
SW1-Zg(config-line)# login           #permite que o user entre
SW1-Zg(config-line)# end

```

(fazer o mesmo para os restantes switches)

#### 2.2- Configurar password para aceder a privileged EXEC access
```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# enable secret cisco
SW1-Zg(config)# exit
```

(fazer o mesmo para os restantes switches)

#### 2.3- Configurar password para VTY (Virtual Terminal)
Virtual Terminal (VTY) lines permite aceder remotamente, com Telnet ou SSH, a um dispositivo. 
Para assegurar VTY lines, é necessário:

```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# line vty 0 15          #comando para configurar 15 lines 
SW1-Zg(config)# password cisco         #cria password
SW1-Zg(config-line)# login
SW1-Zg(config-line)# end
```
(fazer o mesmo para os restantes switches)

#### 2.4- Encriptar as Passwords
Os ficheiros de startup-config e running-config mostram as passwords em texto aberto. Para encriptar as password é preciso:

```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# service password-encryption
```
(fazer o mesmo para os restantes switches)


<b> Pode-se ver a running-config com: </b>
```
show running-config
```

<b> Pode-se ver a startup-config com: </b>
```
show startup-config
```

### 3- Configurar mensagem de introdução (banner) para os <span style="color: #3594FF">switches</span>

```
SW1-Zg> enable
SW1-Zg# configure terminal
SW1-Zg(config)# banner motd #Authorized Access Only#
```
(fazer o mesmo para os restantes switches)


### 4- Ficheiros de configuração para os <span style="color: #3594FF">switches</span>

A running-config fica armazenada em RAM. Para ser possível tornar as configurações definitivas, é necessário copiar para a startup-config (armazenada em NVRAM):

```
SW1-Zg> enable
SW1-Zg# copy running-config startup-config
```
#### 4.1- Apagar ficheiros de configuração
Se as mudanças da running config não estiverem de acordo com o que é suposto (e ainda não foram guardadas em NVRAM), é possível repôr a configuração para a última configuração, com reload:

```
SW1-Zg> enable
SW1-Zg# reload
```

Se as mudanças já foram armazenas em NVRAM, é necessário eliminar todas as configurações e fazer restart ao dispositivo:

```
SW1-Zg> enable
SW1-Zg# erase startup-config
SW1-Zg# reload
```

### 5- VLAN e SSH num Switch

<b>VLAN IPv4:</b>
```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# interface vlan1
SW1-Zg(config-if)# ip address <ip> <subnet-mask>
SW1-Zg(config-if)# no shut
SW1-Zg(config-if)# exit
SW1-Zg(config)# ip default-gateway <gateway_IP_address>
```

<b>VLAN IPv6:</b>
<br><b>Nota: certificar que o SDM do switch é dual-ipv4-and-ipv6</b>
```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# interface vlan1
SW1-Zg(config-if)# ipv6 address <ip> <subnet-mask>
SW1-Zg(config-if)# no shut
SW1-Zg(config-if)# exit
SW1-Zg(config)# ipv6 route ::/0 <gateway_IP_address>
```

<b>SSH:</b>
```
SW1-Zg> enable
SW1-Zg# conf t
SW1-Zg(config)# no ip domain-lookup
SW1-Zg(config)# hostname SW1-Zg
SW1-Zg(config)# ip domain-name isepacademy.ccna.itn.com
SW1-Zg(config)# security passwords min-length 5
SW1-Zg(config)# service password-encryption
SW1-Zg(config)# enable secret class
SW1-Zg(config)# username cisco secret class
SW1-Zg(config)# crypto key generate rsa generate-keys modulus 2014
SW1-Zg(config)# line vty 0 4
SW1-Zg(config-line)# login local
SW1-Zg(config-line)# transport input ssh

```

## <span style="color: #65FF4E">Configuração Básica de Routers</span>

### 1- Configurar o nome do <span style="color: #65FF4E">router</span>
```
Router> enable
Router# conf t
Router(config)# hostname RT1-Zg
```

### 2- Configurar o password do privileged EXEC mode do <span style="color: #65FF4E">router</span>

```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# enable secret cisco
```

### 3- Configurar o password do EXEC mode do <span style="color: #65FF4E">router</span>

```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# line console 0
RT1-Zg(config-line)# password cisco
RT1-Zg(config-line)# login
```

### 3- Configurar o password do acesso ao <span style="color: #65FF4E">router</span> através de Telnet/SSH

```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# line console 0
RT1-Zg(config-line)# line vty 0 4
RT1-Zg(config-line)# password cisco
RT1-Zg(config-line)# login
RT1-Zg(config-line)# transport input {ssh | telnet}
```

### 4- Encriptar todas as passwords
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# line console 0
RT1-Zg(config-line)# exit
RT1-Zg(config)# service password-encryption
```

### 5- Mostrar informação legal
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# banner motd delimiter message delimiter
```

### 6- Guardar configurações dos routers
```
RT1-Zg# copy running-config startup-config
```

## Configurar interfaces do Router

### 1- Configurar interface do router
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# interface type-and-number
RT1-Zg(config-if)# description description-text
RT1-Zg(config-if)# ip address ipv4-address subnet-mask
RT1-Zg(config-if)# ipv6 address ipv6-address/prefix-length
RT1-Zg(config-if)# no shutdown
```

### 2- Verificar configurações do router

#### Mostrar os IPs das interfaces e o estado atual:
```
RT1-Zg> enable
RT1-Zg# show ip interface brief        #ipv4
RT1-Zg# show ipv6 interface brief      #ipv6
```

#### Mostrar o conteúdo das tabelas de routing em RAM
```
RT1-Zg> enable
RT1-Zg# show ip route                  #ipv4
RT1-Zg# show ipv6 route                #ipv6
```

#### Mostrar as estatísticas de todas as interfaces do dispositivo (só IPv4)
```
RT1-Zg> enable
RT1-Zg# show interfaces
```

#### Mostrar as estatísticas de todas as interfaces do router
```
RT1-Zg> enable
RT1-Zg# show ip interface               #ipv4
RT1-Zg# show ipv6 interface             #ipv6
```

### 3- Configurar ligação entre dois Routers com static routing

Zagreb: 
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# ip route 172.20.4.0(endereço da rede remota) 255.255.255.192 (mascara da rede remota) 10.0.0.2 (endereço do next hop router)
```

```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# ip route 172.20.11.0(endereço da rede remota) 255.255.255.0 (mascara da rede remota) 10.0.0.6 (endereço do next hop router)
```

Pula:
```
RT1-Pl> enable
RT1-Pl# conf t
RT1-Pl(config)# ip route 172.20.3.0(endereço da rede remota) 255.255.255.128 (mascara da rede remota) 10.0.0.1 (endereço do next hop router)
```

(etc)


### 4- Configurar SSH (Parte 3 do trabalho)

#### 1- Configurar um hostname único
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# hostname RT1-Zg
```
#### 2- Configurar o IP domain name: 

```
RT1-Zg> enable
RT1-Zg# conf t
R1(config)# ip domain name isepacademy.ccna.itn.com
```
#### 3- Criar uma chave para encriptar o tráfego SSH
SSH encripta o tráfego entre source e destination. Contudo, é necessária uma chave única de autenticação.

```
RT1-Zg(config)# crypto key generate rsa general-keys modulus 1024
```

#### 4- Criar um utilizador
```
RT1-Zg(config)# username cisco secret class
```

#### 5- Autenticar
```
RT1-Zg(config)# line vty 0 4
RT1-Zg(config-line)# login local
```

#### 6- Permitir vty inbound sessions
```
R1(config-line)# transport input ssh
```

<b>Nota: é melhor seguir este tutorial</b>

### 5- Configurar loopbacks
```
RT1-Zg> enable
RT1-Zg# conf t
RT1-Zg(config)# interface loopback <number>
RT1-Zg(config)# ip address <IP_address> <subnet_mask>
```
