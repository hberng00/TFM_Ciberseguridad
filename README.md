# TFM_Ciberseguridad

Este repositorio contiene una serie de archivos basados en material originalmente creado por la **Open Networking Foundation (ONF)** y posteriormente modificados para adaptarse a los requisitos del laboratorio empleado en el Trabajo Fin de Máster.  
El objetivo es documentar la configuración utilizada para desplegar y asegurar un entorno 5G compuesto por gNB, UE simulado, SD-Core y conexión mediante VPN.

---

## 📁 Archivos incluidos

### **hosts.ini**
Archivo de inventario utilizado por Ansible.  
Define el mini PC como host del core 5G, incluyendo su dirección IP y los parámetros necesarios para establecer la conexión y ejecutar el despliegue automatizado.

---

### **main.yml**
Playbook principal encargado de configurar el entorno del gNB y proporcionar variables al resto de archivos del core 5G, incluida la dirección IP y la interfaz de red.

Cuando se utiliza la VPN, puede producirse un conflicto al aplicar estas variables en ciertos componentes, como el AMF:

- **Sin conflicto:**  
  La IP del AMF se actualiza desde `main.yml`, asignando la correspondiente a la interfaz VPN.

- **Con conflicto:**  
  `main.yml` se mantiene sin cambios y la variable problemática se elimina de ese componente.  
  La IP se fija directamente en el archivo de configuración del core afectado.

---

### **sdcore-5g-values.yaml**
Archivo de configuración para SD-Core.  
Modificaciones realizadas:

- Desactivación del **SCTP Load Balancer**.  
- Ampliación de la configuración del **AMF mediante NGAP**, adaptándola a los requisitos del laboratorio.

En caso de conflicto con la variable IP procedente de `main.yml` (especialmente cuando se usa VPN), este archivo puede modificarse directamente para definir la IP correcta de la interfaz `tun` hacia el AMF.

---

### **netpol.yaml**
Archivo que contiene las **NetworkPolicies** utilizadas para controlar la comunicación entre los distintos pods del core 5G.  
Permite segmentar el tráfico e implementar un control más estricto de qué servicios pueden comunicarse entre sí.

---

### **client.conf**
Archivo de configuración del **cliente OpenVPN**.  
Incluye los parámetros necesarios para que el gNB o el mini PC se conecten al servidor VPN, como la dirección del servidor, certificados, claves y ajustes de cifrado.

---

### **server.conf**
Archivo de configuración del **servidor OpenVPN**.  
Define el funcionamiento del servicio VPN, gestionando las conexiones de los clientes, las direcciones IP virtuales, certificados del servidor y parámetros de seguridad.

---

### **custom-gnb.yaml**
Archivo de configuración del **gNB personalizado**.  
Incluye parámetros como la IP del AMF, el PLMN, la interfaz de red y otros ajustes necesarios para conectar el gNB al core 5G, especialmente cuando se utiliza la VPN.

---

### **custom-ue.yaml**
Archivo de configuración del **UE simulado**.  
Contiene las credenciales del UE, el PLMN y los parámetros de comportamiento utilizados para las pruebas de registro y conectividad en el entorno 5G.

---

### **README.md**
Documento descriptivo del repositorio y de los archivos incluidos.

---
