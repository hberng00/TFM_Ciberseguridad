# TFM_Ciberseguridad

Este repositorio contiene archivos originalmente creados p# TFM_Ciberseguridad

Este repositorio contiene una serie de archivos basados en material originalmente creado por la **Open Networking Foundation (ONF)**, los cuales han sido adaptados para ajustarse a los requisitos del laboratorio utilizado en el Trabajo Fin de Máster.  
A continuación se describen los archivos incluidos y las modificaciones realizadas.

---

## Archivos incluidos

### hosts.ini
Archivo de inventario utilizado por Ansible.  
Incluye la información necesaria para definir el mini PC como host del core 5G, especificando la dirección IP y los parámetros de acceso correspondientes.

---

### main.yml
Playbook principal encargado de configurar el entorno del gNB y de suministrar variables al resto de archivos del core 5G, incluida la dirección IP y la interfaz de red.

Cuando se utiliza la VPN, puede ocurrir un conflicto al aplicar estas variables en ciertos componentes del core, como el AMF.

- **Si no se produce conflicto:**  
  La IP del AMF se actualiza normalmente desde `main.yml`, asignando la dirección correspondiente a la interfaz utilizada por la VPN.

- **Si se produce conflicto:**  
  Se mantiene `main.yml` sin cambios y la variable correspondiente deja de utilizarse en el componente afectado.  
  En su lugar, la IP se fija directamente en el archivo de configuración del core que requiera la modificación.

---

### sdcore-5g-values.yaml
Archivo de configuración para SD-Core.  
Modificaciones realizadas:

- Desactivación del SCTP Load Balancer.  
- Ampliación de la configuración del AMF mediante NGAP, adaptada a los requisitos del laboratorio.

En caso de conflicto con la variable proporcionada desde `main.yml`, este archivo puede ser modificado directamente para incluir la dirección IP fija requerida por el AMF.

---

### netpol.yaml
Archivo que define las NetworkPolicies utilizadas para controlar la comunicación entre los distintos pods del core 5G.  
Establece qué servicios pueden comunicarse entre sí, proporcionando segmentación y mayor control del tráfico interno.

---

### README.md
Documento descriptivo del repositorio y de los archivos incluidos.  
Esta versión ofrece una explicación clara y coherente del propósito y funcionamiento de cada archivo del proyecto.
or la **Open Networking Foundation (ONF)** y posteriormente modificados para adaptarse a los requisitos del laboratorio. A continuación se describen los archivos incluidos y las adaptaciones realizadas.

---

## Archivos

### **hosts.ini**
Archivo de inventario Ansible.  
Incluye la información específica del mini PC (dirección IP y parámetros necesarios) para definirlo como host del core 5G.

### **main.yml**
Playbook principal utilizado para gestionar la configuración del entorno del gNB.  
Se ha modificado para incorporar la interfaz de red y la dirección IP del mini PC.
Según se este o no utilizando la vpn se pondra la ip de la intefaz correspondiente.

### **sdcore-5g-values.yaml**
Archivo de configuración para SD-Core.  
Modificaciones realizadas:
- Desactivación del **SCTP Load Balancer**.  
- Extensión de la configuración del **AMF mediante NGAP**, adaptándolo a las necesidades del laboratorio.
Cuando se usa la vpn puede dar probelmas por confiltos al poner la ip en main.yml, si fuera asi se modificaria directamente esete archivo para evitar estos y se pondria la ip directamente al amf de la interfaz tun.

### **netpol.yaml**
Archivo que contiene las **NetworkPolicies** empleadas para controlar las comunicaciones entre los distintos pods del core 5G.  
Define qué servicios pueden comunicarse entre sí para asegurar un mayor control y segmentación del tráfico interno.

### **README.md**
Documento descriptivo del repositorio y de los archivos incluidos.

---
