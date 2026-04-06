## Proyecto Red Local: GIMNASIO

Este repositorio contiene la propuesta integral de diseño y configuración de red local para una empresa de servicios deportivos de alta tecnología. El proyecto ha sido desarrollado para el módulo de Redes Locales dentro del Proyecto Intermodular.

## Descripción del Proyecto
El objetivo es diseñar una infraestructura de red corporativa que integre de forma segura los servicios administrativos de un gimnasio, un ecosistema domótico avanzado para una gestión inteligente (IoT), y una conectividad pública transparente y segura para los clientes.

---

## 1. Análisis de Necesidades
Para el correcto funcionamiento del gimnasio, se han identificado y cubierto las siguientes necesidades de red:
* **Gestión Administrativa:** Conectividad para PCs de recepción y administración destinados al registro de socios ,facturación y compartición de recursos en red (impresoras y archivos de gestión) dentro de la VLAN 10..
* **Control de Acceso:** Integración de tornos inteligentes que requieren comunicación constante con la base de datos para validación de entradas.
* **Infraestructura IoT:** Despliegue de webcams de seguridad, sensores de humo, ventiladores automatizados y altavoces para hilo musical, todos centralizados para una gestión remota.
* **Servicio al Cliente:** Necesidad de una red inalámbrica independiente para que los socios consulten sus rutinas sin comprometer la seguridad de los equipos internos.

---

## 2. Diagrama de Topología de Red
Se ha optado por una topología física en estrella segmentada lógicamente para garantizar la disponibilidad. Un fallo en un cable individual no afecta al resto de la infraestructura.

#### Mapa Visual de la Infraestructura
**GENERAL:**

<img width="2324" height="1020" alt="image" src="https://github.com/user-attachments/assets/8eb57aec-5b24-476d-ab47-f229a23478ac" />

**SWITCH:**

<img width="814" height="177" alt="image" src="https://github.com/user-attachments/assets/5430b32f-f49c-445a-8c05-dc1ce3fe779a" />

**ROUTER:**

<img width="683" height="417" alt="image" src="https://github.com/user-attachments/assets/50606e02-895c-4233-b4a0-55e7775a3fc8" />

---

## 3. Arquitectura y Tecnologías
La simulación se ha realizado con Cisco Packet Tracer. Los componentes clave son:

* **Capa de Distribución:** Router 4331 gestionando subinterfaces y Switch 2960-24TT para la conmutación de VLANs bajo el estándar 802.1Q.
* **Capa de Acceso:** Mezcla de dispositivos finales (PCs, Portatiles), dispositivos de infraestructura IoT y terminales de control de acceso.
* **Movilidad:** Despliegue de múltiples Puntos de Acceso (AP) configurados para extender la cobertura inalámbrica de forma transparente.

---

## 4. Plan de Direccionamiento IP (/24)
La red se ha segmentado en tres VLANs lógicas para aislar el tráfico y aplicar políticas de seguridad.

| VLAN | Nombre | Subred (Red: 192.10.x.0) | Gateway (Router) | Propósito de la Red |
| :--- | :--- | :--- | :--- | :--- |
| **10** | GESTIÓN | 192.10.10.0 /24 | 192.10.10.1 | PCs Administrativos y Tornos de acceso. |
| **20** | IOT | 192.10.20.0 /24 | 192.10.20.1 | Domótica (Webcams, Sensores, Altavoces, Ventiladores). |
| **30** | CLIENTES | 192.10.30.0 /24 | 192.10.30.1 | WiFi público para Smartphones y Tablets. |

---

## 5. Servicios y Seguridad (ACL)
Para garantizar la integridad y el cumplimiento de normativas de seguridad, se han implementado:

* **DHCP Dinámico:** Asignación automática de direccionamiento IP para dispositivos de clientes e IoT, facilitando la administración.
* **Enrutamiento Inter-VLAN:** Configurado en el Router para permitir que la administración (VLAN 10) monitorice y gestione los dispositivos IoT (VLAN 20).
* **Aislamiento de Clientes (Seguridad):** Se ha configurado una Lista de Control de Acceso (ACL) extendida. Esta política permite a la VLAN 30 el acceso a internet pero bloquea estrictamente la comunicación con las VLANs privadas (10 y 20).

---

## 6. Pruebas de Funcionamiento (Testing)

### Flujo 1: Conectividad Interna (Gestión a IoT)
Prueba exitosa que demuestra que los servicios privados (ej: PC de recepción) pueden monitorizar los equipos domóticos (ej: una Webcam). El primer paquete puede fallar por resolución ARP, obteniendo éxito total en los siguientes.

<img width="891" height="688" alt="image" src="https://github.com/user-attachments/assets/14eea0ef-4143-4489-9ce4-648e3fd4ee02" />

---

### Flujo 2: Bloqueo de Seguridad (Clientes a Red Privada)
Demostración del aislamiento de seguridad mediante ACL. Un Smartphone intenta conectarse a la red de administración y el Router bloquea el tráfico devolviendo "Destination host unreachable".

<img width="886" height="688" alt="image" src="https://github.com/user-attachments/assets/e2461671-9877-469f-bac3-b80610b6b0e8" />

---
