# Topología de Red e Infraestructura

## Componentes

### 1. Firewall Perimetral (pfSense)
* Interfaz WAN: `192.168.100.1/24` (Red externa).
* Interfaz LAN: `192.168.1.1/24` (Segmento interno del laboratorio).
* Interfaz OPT1: `192.168.56.2` (Red Host-Only para gestión).

### 2. Servidor SIEM (Ubuntu & Wazuh)
* Adaptador `enp0s3` (LAN): `192.168.1.10/24` (Puerta de enlace: pfSense `192.168.1.1`).
* Adaptador `enp0s8` (Host-Only): Canal de administración.

## Especificaciones Técnicas

* **Persistencia de Red (Netplan):** El servicio `cloud-init` se encuentra deshabilitado para evitar sobrescrituras de configuración.
* **Ruta de Configuración:** Centralizada en `/etc/netplan/01-netcfg-lab.yaml`.
* **Permisos del Sistema:** Archivo protegido con permisos estrictos mediante `chmod 600`.
* **Panel de Control (Wazuh Dashboard):** Operativo y accesible mediante HTTPS.
