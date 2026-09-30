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
4. Validar la sintaxis del archivo de configuración
```
sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf
```
5. Reiniciar el servicio DHCP y comprobar su estado
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
