# DMZ Lab - 4geeks

## Descripción

Este repositorio contiene el desarrollo del laboratorio **Construyendo y Asegurando una Red con una Zona Desmilitarizada** realizado en Cisco Packet Tracer para el Bootcamp de Ciberseguridad de 4geeks.

El objetivo del laboratorio fue implementar una DMZ utilizando un router Cisco ISR, configurando el direccionamiento IP, NAT estático y listas de control de acceso (ACL) para permitir el acceso controlado a un servidor web ubicado en la DMZ, mientras se protege la red interna frente a accesos no autorizados.

---

## Objetivos del laboratorio

* Configurar el direccionamiento IP de todos los dispositivos.
* Implementar una Zona Desmilitarizada (DMZ).
* Publicar un servidor web mediante NAT estático.
* Controlar el tráfico entre la LAN, la DMZ y la red externa utilizando ACL.
* Verificar el correcto funcionamiento mediante pruebas de conectividad y acceso web.

---

## Contenido del repositorio

```text
dmz-lab/
│
├── DMZ_PROJECT.pkt
├── README.md
├── informe/
│   └── Informe_DMZ_Laboratorio.md
└── evidencias/
    ├── 01_topologia.png
    ├── 02_show_ip_interface_brief.png
    ├── 03_show_access_lists.png
    ├── 04_ping_pc_internal_gateway.png
    ├── 05_acceso_web_pc_external.png
    ├── 06_bloqueo_dmz_lan.png
    └── 07_assessment_final.png
```

---

## Resultados obtenidos

Al finalizar el laboratorio se comprobó que:

* La conectividad entre las tres redes funcionaba correctamente.
* El servidor web de la DMZ era accesible desde la red externa mediante NAT.
* La red interna podía acceder al servidor de la DMZ.
* El tráfico desde la DMZ hacia la LAN era bloqueado mediante ACL, manteniendo el aislamiento de la red interna.

---

## Autor

**Facundo López Reguera**
