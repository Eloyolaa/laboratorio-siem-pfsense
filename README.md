# Laboratorio de Ciberseguridad: SIEM Wazuh, Firewall pfSense y Kali Linux

Entorno controlado de red diseñado para simular ataques externos, auditoría perimetral y correlación de eventos en tiempo real mediante un SIEM de nivel empresarial.

## Topología y Arquitectura General

```mermaid
graph TD
    subgraph HostWindows [PC Anfitrión / Windows]
        Browser[Navegador Web / Dashboard y WebGUI]
    end

    subgraph Hipervisor [VirtualBox]
        subgraph WAN [Red Externa]
            Kali[Kali Linux / Atacante / 192.168.100.x]
        end

        pfSense[pfSense / WAN: 192.168.100.1 / LAN: 192.168.1.1]

        subgraph LAN [Red Interna]
            Ubuntu[Ubuntu Server / Wazuh / 192.168.1.10]
        end

        Kali -->|Tráfico Externo| pfSense
        pfSense -->|Segmentación| Ubuntu
        Browser -.->|Gestión| pfSense
        Browser -.->|Gestión SIEM| Ubuntu
    end
