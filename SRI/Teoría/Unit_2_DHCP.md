UBUNTU
SERVIDOR

1. Identificar interfaz de red y su IP estática (enp0s3 -> 172.16.5.140/24)
```
ip a
```
2. Configurar la interfaz de escucha en INTERFACESv4="enp0s3"
```
sudo nano /etc/default/isc-dhcp-server
```
3. Configurar la subred (172.16.5.0/24) y el rango de emisión (172.16.5.150 a 172.16.5.200)
```
sudo nano /etc/dhcp/dhcpd.conf
```
4. Dentro del archivo añadimos al final del todo la siguiente línea.
   ```
   subnet 172.16.5.0 netmask 255.255.255.0 {
    range 172.16.5.150 172.16.5.200;
    default-lease-time 600;
    max-lease-time 7200;
} 
```
5. Validar la sintaxis del archivo de configuración
```
sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf
```
6. Reiniciar el servicio DHCP y comprobar su estado
```
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server
```
CLIENTE

1. Configurar la interfaz (enp0s3) para solicitar IP dinámica (dhcp4: true)
```
sudo nano /etc/netplan/cloud50-init.yaml
```
2. Aplicar la configuración de red
```
sudo netplan apply
```
3. Verificar la IP asignada por el servidor (172.16.5.151)
```
ip a
```

WINDOWS y UBUNTU cliente



SERVIDOR (WINDOWS SERVER 2022)

1. Configurar la interfaz de red con IP estática (Ethernet -> 172.16.5.149/24)
Administrador del servidor -> Servidor local -> Ethernet -> Propiedades -> IPv4
Dirección IP: 172.16.5.149
Máscara de subred: 255.255.255.0


2. Instalar el rol de Servidor DHCP
Administrador del servidor -> Administrar -> Agregar roles y características
Instalación basada en características o en roles -> Seleccionar Servidor -> Marcar "Servidor DHCP" -> Instalar


3. Completar la configuración post-instalación y autorizar el servicio
Administrador del servidor -> Notificaciones (Icono Bandera) -> Completar configuración de DHCP -> Autorizar


4. Crear y activar el ámbito IPv4 (Red_Clientes_Ubuntu)
Administrador del servidor -> Herramientas -> DHCP
IPv4 (clic derecho) -> Ámbito nuevo...
Rango: 172.16.5.50 a 172.16.5.200
Máscara: 255.255.255.0 (/24)
Activar ámbito: Sí


5. Permitir peticiones ICMPv4 (Ping) en el Firewall de Windows
Herramientas -> Windows Defender Firewall con seguridad avanzada -> Reglas de entrada
Buscar "Archivos e impresoras compartidos (petición eco: ICMPv4 de entrada)" -> Propiedades -> Habilitar regla


CLIENTE (UBUNTU)

1. Instalar cliente DHCP tradicional
```
sudo apt update
sudo apt install isc-dhcp-client
```

3. Solicitar y renovar la dirección IP mediante DHCP
```
sudo dhclient -r
sudo dhclient
```

4. Verificar la IP dinámica asignada por el servidor (172.16.5.193)
```
ip a
```

5. Comprobar conectividad con el servidor Windows Server
```
ping -c 4 172.16.5.149
```
