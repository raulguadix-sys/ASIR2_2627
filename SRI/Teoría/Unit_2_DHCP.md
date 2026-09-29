SERVIDOR
# 1. Identificar interfaz de red (ej. enp0s3)
```
ip a
```
# 2. Configurar IP estática (192.168.1.1/24)
```
sudo nano /etc/netplan/50-cloud-init.yaml
sudo chmod 600 /etc/netplan/50-cloud-init.yaml
sudo netplan apply
```
# 3. Instalar servidor DHCP
```
sudo apt update && sudo apt install isc-dhcp-server -y
```
# 4. Asignar interfaz de escucha en INTERFACESv4="enp0s3"
```
sudo nano /etc/default/isc-dhcp-server
```
# 5. Definir el rango DHCP en subnet 192.168.1.0
```
sudo nano /etc/dhcp/dhcpd.conf
```
# 6. Iniciar el servicio y comprobar concesiones
```
sudo systemctl restart isc-dhcp-server
cat /var/lib/dhcp/dhcpd.leases
```
CLIENTE
# 1. Configurar red para pedir IP por DHCP (dhcp4: true)
```
sudo nano /etc/netplan/cloud50-init.yaml
sudo chmod 600 /etc/netplan/cloud50-init.yaml
```
# 2. Aplicar y solicitar IP al servidor
```
sudo netplan apply
```
# 3. Verificar IP recibida y probar conexión
```
ip a
ping 192.168.1.1
```
