# Laboratorio de Ciberseguridad: SIEM Wazuh, Firewall pfSense y Kali Linux

##  Objetivo del Laboratorio
Diseñar, implementar y documentar un entorno controlado de red para analizar el comportamiento del tráfico malicioso, el filtrado perimetral y la detección de intrusiones utilizando un SIEM de nivel empresarial.

---

##  Configuración de Red e Infraestructura

### 1. Firewall Perimetral (pfSense)
* **Interfaz WAN:** Conectada a la red externa con la dirección `192.168.100.1/24`.
* **Interfaz LAN:** Configurada con la puerta de enlace `192.168.1.1` para aislar, segmentar y enrutar el tráfico del laboratorio (`192.168.1.0/24`).

### 2. Servidor SIEM (Ubuntu Server & Wazuh)
El servidor opera bajo una arquitectura de **doble adaptador de red** para separar el tráfico analítico del canal de administración:
* **`enp0s3` (Red Interna - Laboratorio):** Configurado con la IP estática `192.168.1.10/24` y enrutamiento apuntando al pfSense (`192.168.1.1`).
* **`enp0s8` (Host-Only - Administración):** Interfaz dedicada para la gestión y acceso directo desde el equipo anfitrión.

---

##  Especificaciones Técnicas

* **Persistencia de Red (Netplan):** El servicio `cloud-init` se encuentra deshabilitado para evitar sobrescrituras, centralizando la configuración en el archivo `/etc/netplan/01-netcfg-lab.yaml` bajo permisos estrictos (`chmod 600`).
* **Panel de Control (Wazuh Dashboard):** Accesible a través de la interfaz de gestión local.

---

##  Arquitectura de Red y Topología

```mermaid
graph TD
    subgraph HostWindows [PC Administración / Windows]
        Browser[Navegador Web <br/> Wazuh Dashboard & pfSense WebGUI]
    end

    subgraph Hipervisor [VirtualBox / VMware]
        subgraph WAN [Red Externa / Untrusted]
            Kali[Kali Linux <br/> Máquina Atacante <br/> IP: 192.168.x.x]
        end

        pfSense[pfSense Firewall / Router <br/> WAN: 192.168.100.1 <br/> LAN: 192.168.1.1]

        subgraph LAN [Red Interna / Trusted]
            Ubuntu[Servidor Ubuntu <br/> Wazuh Manager & Agente <br/> IP: 192.168.1.10]
        end

        Kali -->|Ataques / Escaneos / Tráfico Externo| pfSense
        pfSense -->|Inspección / Reglas de Bloqueo| Ubuntu
        Browser -.->|Acceso Administrativo| pfSense
        Browser -.->|Acceso a Consola SIEM| Ubuntu
    end

