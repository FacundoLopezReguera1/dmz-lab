
# Informe de configuración de DMZ con Cisco Packet Tracer


### 1. Objetivo del laboratorio

El objetivo de este laboratorio fue configurar una Zona Desmilitarizada (DMZ) utilizando un router Cisco ISR en Cisco Packet Tracer. Para esto, se implementó una red dividida en tres zonas (LAN, DMZ y red externa), se configuró el NAT estático para publicar un servidor web y se aplicaron listas de control de acceso (ACL), para controlar el tráfico permitido entre las diferentes redes y proteger la red interna frente a accesos no autorizados.

---

### 2. Topología implementada

> Describe la red. Puedes incluir una imagen si el software lo permite (captura de Packet Tracer).

- Cantidad de redes: 3
- Dispositivos usados: 
    - 1 Router Cisco ISR 2911 (Router_FW)
    - 3 Switches Cisco 2960
    - 1 PC_Internal
    - 1 Server_DMZ (Servidor Web)
    - 1 PC_External
- Breve descripción de la función de cada zona (LAN, DMZ, Externa) :
    - **LAN:** Red interna donde se encuentra el equipo del usuario. Tiene acceso al servidor de la DMZ, pero permanece protegida de accesos directos desde otras redes.
    - **DMZ:** Red destinada a alojar el servidor web. Puede ser accedida desde la red externa mediante NAT, mientras permanece aislada de la red interna.
    - **Red Externa:** Simula Internet. Desde esta red únicamente se permite el acceso al servicio web publicado mediante NAT.

---

### 3. Plan de direccionamiento IP

Completa la tabla con las IPs asignadas (puedes copiarla del enunciado si no cambió).

| Dispositivo             | IP               | Máscara           | Gateway           |
|-------------------------|------------------|-------------------|-------------------|
| PC_Internal             |192.168.1.10      |255.255.255.0      |192.168.1.1        |
| Server_DMZ              |192.168.2.10      |255.255.255.0      |192.168.2.1        |
| PC_External             |192.168.3.10      |255.255.255.0      |192.168.3.1        |
| Router_FW Gi0/0 (LAN)   |192.168.1.1       |255.255.255.0      |         -         |
| Router_FW Gi0/1 (DMZ)   |192.168.2.1       |255.255.255.0      |         -         |
| Router_FW Gi0/2 (Ext)   |192.168.3.1       |255.255.255.0      |         -         |

---

### 4. Configuración aplicada (resumen)

> Resume los comandos o pasos más relevantes que ejecutaste. Usa texto + fragmentos de código cuando sea necesario.

Se configuraron las interfaces del router, se implementó NAT estático para publicar el servidor web de la DMZ y se aplicaron ACL para controlar el tráfico entre la LAN, la DMZ y la red externa.

- Interfaces configuradas con `ip address`:
    - GigabitEthernet0/0 -> 192.168.1.1/24 (LAN)
    - GigabitEthernet0/1 -> 192.168.2.1/24 (DMZ)
    - GigabitEthernet0/2 -> 192.168.3.1/24 (Red Externa)
    - Se habilitaron todas las interfaces con el comando no shutdown.
    
- NAT:
```bash
ip nat inside
```

```bash
ip nat outside
```

```bash
ip nat inside source static 192.168.2.10 192.168.3.1
```
- ACLs:
```bash
permit tcp any host 192.168.3.1 eq 80
permit tcp any host 192.168.3.1 eq 443

access-list 101 permit tcp any host 192.168.3.1 eq 80
access-list 100 deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255


```

---

### 5. Verificaciones realizadas

> Describe las pruebas y su resultado. Incluye capturas o salidas de comandos si se puede.

- `ping` desde PC_Internal al gateway (192.168.1.1): ✅ Se obtuvo respuesta correctamente, verificando la conectividad de la LAN.
- `ping` desde Server_DMZ al gateway (192.168.2.1): ✅ Se obtuvo respuesta correctamente.
- `ping` desde PC_External al gateway (192.168.3.1): ✅ Se obtuvo respuesta antes de eliminar la regla ICMP de la ACL 101.
- Acceso web desde PC_Internal a http://192.168.2.10: ✅ El servidor web respondió correctamente.
- Acceso web desde PC_External a http://192.168.3.1: ✅ El NAT estático redirigió correctamente la conexión al servidor de la DMZ.
- Bloqueo de acceso desde Server_DMZ hacia PC_Internal mediante ping: ✅ El tráfico fue bloqueado por la ACL 100, verificando el aislamiento de la DMZ.
- Bloqueo de ping desde PC_External hacia 192.168.3.1 después de eliminar la regla ICMP de la ACL 101: ✅ El acceso ICMP fue bloqueado, mientras que el acceso HTTP continuó funcionando correctamente.

---

### 6. Conclusiones y recomendaciones

> ¿Qué aprendiste con este ejercicio? ¿Qué mejorarías?

Durante este laboratorio aprendí a configurar una Zona Desmilitarizada (DMZ) utilizando un router Cisco ISR, asignando direcciones IP, implementando NAT estático y aplicando listas de control de acceso (ACL) para restringir el tráfico entre las distintas redes. También comprendí la importancia de verificar la conectividad básica antes de aplicar las reglas de seguridad, ya que un error en la configuración puede afectar el funcionamiento de toda la red.

Como mejora, es conveniente realizar pruebas de conectividad después de cada etapa de la configuración y utilizar comandos de verificación, como `show ip interface brief` y `show access-lists`, para identificar y corregir posibles errores antes de continuar.

---
