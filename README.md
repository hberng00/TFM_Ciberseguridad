# TFM_Ciberseguridad

Este repositorio contiene archivos originalmente creados por la **Open Networking Foundation (ONF)** y posteriormente modificados para adaptarse a los requisitos del laboratorio. A continuación se describen los archivos incluidos y las adaptaciones realizadas.

---

## Archivos

### **hosts.ini**
Archivo de inventario Ansible.  
Incluye la información específica del mini PC (dirección IP y parámetros necesarios) para definirlo como host del core 5G.

### **main.yml**
Playbook principal utilizado para gestionar la configuración del entorno del gNB.  
Se ha modificado para incorporar la interfaz de red y la dirección IP del mini PC.

### **sdcore-5g-values.yaml**
Archivo de configuración para SD-Core.  
Modificaciones realizadas:
- Desactivación del **SCTP Load Balancer**.  
- Extensión de la configuración del **AMF mediante NGAP**, adaptándolo a las necesidades del laboratorio.

### **netpol.yaml**
Archivo que contiene las **NetworkPolicies** empleadas para controlar las comunicaciones entre los distintos pods del core 5G.  
Define qué servicios pueden comunicarse entre sí para asegurar un mayor control y segmentación del tráfico interno.

### **README.md**
Documento descriptivo del repositorio y de los archivos incluidos.

---
