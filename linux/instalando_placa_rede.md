# Instalando uma placa de rede 
---

> Esse passo a passo pode ser utilizado quando o computador tem um dispositivo conectada mas o driver não esta instalado e sem internet para fazer a instalação pelo gerenciador de pacotes.

## 1 - Verificando dispositivo conectado e se a modulo/driver disponivel

*Listando dispositivos pci detectados e se tem driver em uso*

```sh

$ lspci -k 

01:00.0 Network controller: Intel Corporation Wireless 3165 (rev 81)
	Subsystem: Intel Corporation Dual Band Wireless AC 3165
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
	Subsystem: Elitegroup Computer Systems RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
	Kernel driver in use: r8169
	Kernel modules: r8169
    ...
```

*lista dispositivos que contem exatamente *rtl818*  no nome*
```sh
lspci |grep rtl818  
```

*lista dispositivos que contem wireless* _(em letras maiuscula ou minuscula)_
```sh
lspci |grep -i wireless
```

*Lista os dispositivos por nome e ID's*
```sh
$ lspci -vnn | grep -i rtl8185 -A 10
```

*Verificando se há modulos disponiveis para o dispositivo*
```sh
$ lsmod | grep -i rtl
```

*Inserindo o modulo para o kernel*
```sh
$ sudo modprobe rtl8180
```

## 2 - Configurar a conexão Wi-Fi

- A) Usar nmtui (recomendado)

```sh
$ sudo nmtui
#Selecione "Activate a connection" e escolha sua rede Wi-Fi.
```

- B) Usar comandos manualmente
```sh
sudo ip link set wlan0 up  # Ativar interface
sudo iwlist wlan0 scan     # Ver redes disponíveis

# Conecte via nmcli (NetworkManager): 
```

```sh
nmcli dev wifi list
nmcli dev wifi connect "NOME_DA_REDE" password "SENHA"
```

> *Observação*  
> Em algumas situações os drivers podem estar disponiveis de forma genérica ou para varias versões proximas da placa instalada e sendo assim o modulo disponivel pode estar com um "x" no final. Sendo assim suba o modulo disponível.

```sh
sudo modprobe rtl818x
```

## 3. Verificar logs em caso de falha

> Se nada funcionar, verifique os logs do kernel:

```sh
dmesg | grep -i rtl
journalctl -xe | grep -i wifi
```

## 4. Sendo uma distro baseada em debian 

> Baixe o pacote .deb, instale utilizando o dpkg e reinicie o computador. Se não deu certo refaça os passos anteriores já que os drivers foram instalados.

```sh
$ dpkg -i package_name.deb
```

