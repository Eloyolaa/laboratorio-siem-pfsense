# Laboratorio de Ciberseguridad: SIEM Wazuh, Firewall pfSense y Kali Linux

Entorno controlado de red diseñado para simular ataques externos, auditoría perimetral y correlación de eventos en tiempo real mediante un SIEM de nivel empresarial.

## Topología y Arquitectura General

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
