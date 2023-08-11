# Despliegue Automatizado de Moodle sobre vCenter para Chetumal
El presente proyecto tiene como objetivo realizar en minutos el deploy de un ambiente 100% produtivo de Moodle.

## Tecnologías
Este proyecto hace uso de tecnologias como:
- VMware vSphere
- Oracle Linux R9
- Ansible

### Requisitos
- Un cluster de VMware vSphere [vCenter + ESXis]
    - Usuario + contraseña [acceso via gui]
    - IP vCenter
- Un Ansible control
    - Inventario de Infraestructura
    - Codigo de proyecto Moodle_Automatico
- Una cerveza fria
### Modo de uso
Se realizaran llamadas a 5 playbooks, en el siguiente orden:
- crea_vms.yml
- init_base.yml
- instala_apps.yml
- configura_apps.yml
- instala_moodle.yml
- prueba_moodle.yml
![](https://github.com/TICSSMX/Moodle-Automatico/blob/chetumal/Auto_moodle_proceso.jpg)
