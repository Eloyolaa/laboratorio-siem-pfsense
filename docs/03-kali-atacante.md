# Perfil Atacante e Infraestructura Ofensiva (Kali Linux)

## Descripción General
Este documento recopila la configuración del lado atacante dentro del laboratorio. Su propósito es simular amenazas externas, realizar escaneos de reconocimiento y ejecutar pruebas de intrusión para validar la capacidad de detección y respuesta del SIEM y las reglas de filtrado del firewall.

## Parámetros de Red y Conectividad
* **Sistema Operativo:** Kali Linux
* **Interfaz de Red:** Conectada al segmento de red externa (`192.168.100.10`).
* **Puerta de enlace predeterminada:** Apuntando hacia la interfaz WAN de pfSense (`192.168.100.1`).

## Herramientas y Vectores a Evaluar (Previsto)
* Escaneo de puertos y descubrimiento de servicios perimetrales (`Nmap`).
* Auditoría de tráfico y análisis de paquetes.
* Simulación de intrusiones para la generación de alertas en el panel de Wazuh.

---

> **Estado del Documento:** *En progreso — Guía reservada para la próxima fase de pruebas ofensivas y correlación de eventos.*
