# Full Anon Mode by Fz3r0

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/9b85cc34-8e4d-4850-8299-8042638b0167)

## To the point

- Lanzar `Firefox` _(u otro explorador)_ con `Tor` + `ProxyChains`

````sh
## 1. Iniciar servicio tor
service tor start

## 2. Reiniciar servicio tor (cambiar IP pública)
service tor restart

## 3. Detener servicio tor
service tor stop

---

## 1. Opcion1: Cambiar MAC aleatorio
ifconfig eth0 down
macchanger -r eth0
ifconfig eth0 up

## 2. Opcion2: Cambiar MAC manual
ifconfig eth0 down
macchanger --mac=f0:f0:f0:f0:f0:f0 eth0
ifconfig eth0 up

---

## 1. Lanzar proxuchains con firefox
proxychains firefox

---

## Verificar Funcionamiento
proxychains curl ifconfig.me/ip

## Verificar via web:

    ## ipchicken.com 
    ## dnsleaktest.com

````

- Lanzar `nmap` con `Tor` + `ProxyChains`

## Instalación de TOR 

````sh
apt-get install tor
````

## Configurar ProxyChains

````sh
subl /etc/proxychains.conf
````

- En el archivo de configuración en este caso pondré `dynamic` ya que es la más efecitva

````java
dynamic_chain  <<<<---------------||||| :)
#
# Dynamic - Each connection will be done via chained proxies
# all proxies chained in the order as they appear in the list
# at least one proxy must be online to play in chain
# (dead proxies are skipped)
# otherwise EINTR is returned to the app
#
#strict_chain
#
# Strict - Each connection will be done via chained proxies
# all proxies chained in the order as they appear in the list
# all proxies must be online to play in chain
# otherwise EINTR is returned to the app
#
#random_chain
#
# Random - Each connection will be done via random proxy
# (or proxy chain, see  chain_len) from the list.
# this option is good to test your IDS :)
````
- En la parte inferior agregar los puertos del servicio y protocolo TOR que son socks4 (TCP) y socks5 (TCP+UDP+Cliente Servidor):

````java

[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"

# socks4 	127.0.0.1 9050
# socks5 	127.0.0.1 9050




````

Para usar proxychains correctamente, debe completar su archivo proxychains.conf con proxies válidos. La razón por la que recibe la respuesta `!!!!need more proxys!!!` es porque no hay proxies en el archivo `proxychains.conf` o los que están configurados ya no están disponibles.

**`IMPORTANTE`: Usar de Proxys alguno de las siguentes listas:**

- https://hidemy.name/en/proxy-list/
- https://vpnoverview.com/privacy/anonymous-browsing/free-proxy-servers/
- https://privatevpn.com/serverlist/
- https://linuxhint.com/proxychains-tutorial/


## Ejecución del servicio `TOR`

1. Comenzar el servicio:

````sh
service tor start
````

2. Revisar servicio:

````sh
service tor status
````

- Se debe mostrar success como a continuación:

````sh
❯ service tor start
❯ service tor status
● tor.service - Anonymizing overlay network for TCP (multi-instance-master)
     Loaded: loaded (/lib/systemd/system/tor.service; disabled; preset: disabled)
     Active: active (exited) since Thu 2023-05-25 23:01:03 EST; 3s ago
    Process: 2590 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 2590 (code=exited, status=0/SUCCESS)
        CPU: 595us

May 25 23:01:03 Fz3r0-D00M systemd[1]: Starting tor.service - Anonymizing overlay network for TCP (mu>
May 25 23:01:03 Fz3r0-D00M systemd[1]: Finished tor.service - Anonymizing overlay network for TCP (mu>
lines 1-9/9 (END)

 ﮊ   /home/fz3r0  took  5s  with   ✘ INT 
````

3. Ejecutar `ProxyChains` en `Firefox` _(salir de modo root)_:

````sh
proxychains firefox
````

## Recursos

- [Navegación Anónima con Tor y ProxyChains en Kali Linux](https://www.youtube.com/watch?v=3UA4Raqqu6I)
- [ProxyChains Tutorial](https://linuxhint.com/proxychains-tutorial/)
