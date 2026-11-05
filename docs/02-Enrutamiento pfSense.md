# Enrutamiento, pfSense y Conectividad

Para permitir la administración de Wazuh desde el equipo Windows hacia la red interna del laboratorio `LAN`, sin romper el aislamiento del firewall, se configuró una red de gestión mediante un adaptador **Host-Only** combinada con una ruta estática y una regla de control de acceso.

## 1. Configuración de Enrutamiento en el Host (Windows)
Ya que el adaptador Host-Only no cuenta con puerta de enlace predeterminada hacia la subred interna del laboratorio (`192.168.1.0/24`), se configuró una ruta estática en el sistema operativo anfitrión:

```cmd
route -p ADD 192.168.1.0 MASK 255.255.255.0 192.168.56.2
