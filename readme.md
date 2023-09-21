# TICSS - VMware - Oracle Linux R9 - Ansible
Implementacion de ambiente para ejecucion de ansible y vmware

## Indice
- Preparación de Ambiente para Ansible
- Validación de Ambiente community.vmware.vm_guest_info
- Creacion de VM de prueba desde un Template

### Preparación de Ambiente

Actualización de Oracle Linux R9

```
sudo yum update -y
```

Instalacion de herramientas para Python

```
sudo yum install python-setuptools git -y
```

Instalacion de pip

```
sudo yum install python-pip -y
```

Finalmente se instala Ansible usando pip

```
sudo pip install ansible 
```

Instalacion de modulo PyVmomi para uso de VMware

```
sudo pip install pyvmomi
```

Instalacion de community.vmware

```
ansible-galaxy collection install community.vmware
pip install -r ~/.ansible/collections/ansible_collections/community/vmware/requirements.txt
```


Verificación

```
ansible localhost -m ping
```

Se debe optener una salida como esta:

```
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

Ahora podemos continuar con la validacion del ambiente...

## Validación de Ambiente

Para realizar la validación del ambiente debemos primero ajustar los archivos: 
- anisble.cfg
- vars.yml
- vm_info.yml

Una ves ajustadas las variables a nuestra infraestructura de VMware, seguimos...

Ejecutanmos el playbook vm_info.yml con el siguiente comando:

```
ansible-playbook -i inventory vm_info.yml
```

Si todo esta bien configurado, debemos obtener una respuesta favorable del vCenter Server.
Algo asi...

```
[ansible@ansible Community.VMware.TICSS]$ ansible-playbook -i inventory vm_info.yml

PLAY [info vm demo] ******************************************************************************************************************************************

TASK [include_vars] ******************************************************************************************************************************************
ok: [localhost]

TASK [get VM info] *******************************************************************************************************************************************
ok: [localhost]

TASK [print VM info] *****************************************************************************************************************************************
ok: [localhost] => {
    "detailed_vm_info": {
        "changed": false,
        "failed": false,
        "instance": {
            "advanced_settings": {
                "ethernet0.exposeLargeBAR": "TRUE",
                "ethernet0.pciSlotNumber": "192",
                "hpet0.present": "TRUE",
                "migrate.hostLog": "Unicornio-7b14a532.hlog",
                "migrate.hostLogState": "none",
                "migrate.migrationId": "0",
                "monitor.phys_bits_used": "45",
                "numa.autosize.cookie": "10012",
                "numa.autosize.vcpu.maxPerVirtualNode": "1",
                "nvram": "Unicornio.nvram",
                "pciBridge0.pciSlotNumber": "17",
                "pciBridge0.present": "TRUE",
                "pciBridge4.functions": "8",
                "pciBridge4.pciSlotNumber": "21",
                "pciBridge4.present": "TRUE",
                "pciBridge4.virtualDev": "pcieRootPort",
                "pciBridge5.functions": "8",
                "pciBridge5.pciSlotNumber": "22",
                "pciBridge5.present": "TRUE",
                "pciBridge5.virtualDev": "pcieRootPort",
                "pciBridge6.functions": "8",
                "pciBridge6.pciSlotNumber": "23",
                "pciBridge6.present": "TRUE",
                "pciBridge6.virtualDev": "pcieRootPort",
                "pciBridge7.functions": "8",
                "pciBridge7.pciSlotNumber": "24",
                "pciBridge7.present": "TRUE",
                "pciBridge7.virtualDev": "pcieRootPort",
                "sched.swap.derivedName": "/vmfs/volumes/62c77110-c32f2a19-aa7c-0010188c4fb8/Unicornio/Unicornio-294dc610.vswp",
                "scsi0.pciSlotNumber": "160",
                "scsi0.sasWWID": "50 05 05 69 24 dc 5f e0",
                "scsi0:0.redo": "",
                "softPowerOff": "FALSE",
                "svga.guestBackedPrimaryAware": "TRUE",
                "svga.present": "TRUE",
                "viv.moid": "91c80e2a-81d7-4e40-9189-b980923386a4:vm-62:fWF3A2Wfr88uGb3XcArvCd8nN1FFuUQ9ZMLcm6xhBdI=",
                "vmotion.checkpointFBSize": "4194304",
                "vmotion.checkpointSVGAPrimarySize": "4194304",
                "vmotion.svga.graphicsMemoryKB": "4096",
                "vmotion.svga.mobMaxSize": "4194304",
                "vmware.tools.internalversion": "0",
                "vmware.tools.requiredversion": "11365"
            },
            "annotation": "",
            "current_snapshot": null,
            "customvalues": {},
            "guest_consolidation_needed": false,
            "guest_question": null,
            "guest_tools_status": "guestToolsNotRunning",
            "guest_tools_version": "0",
            "hw_cluster": "Cluster01",
            "hw_cores_per_socket": 1,
            "hw_datastores": [
                "HDD-free"
            ],
            "hw_esxi_host": "esxi01.home",
            "hw_eth0": {
                "addresstype": "assigned",
                "ipaddresses": null,
                "label": "Network adapter 1",
                "macaddress": "00:50:56:b7:e4:bc",
                "macaddress_dash": "00-50-56-b7-e4-bc",
                "portgroup_key": null,
                "portgroup_portkey": null,
                "summary": "DC"
            },
            "hw_files": [
                "[HDD-free] Unicornio/Unicornio.vmx",
                "[HDD-free] Unicornio/Unicornio.nvram",
                "[HDD-free] Unicornio/Unicornio.vmsd",
                "[HDD-free] Unicornio/vmware.log",
                "[HDD-free] Unicornio/Unicornio.vmdk"
            ],
            "hw_folder": "/izt750/vm/lab",
            "hw_guest_full_name": null,
            "hw_guest_ha_state": null,
            "hw_guest_id": null,
            "hw_interfaces": [
                "eth0"
            ],
            "hw_is_template": false,
            "hw_memtotal_mb": 1024,
            "hw_name": "Unicornio",
            "hw_power_status": "poweredOn",
            "hw_processor_count": 1,
            "hw_product_uuid": "4237c159-24dc-5fec-3e47-b0f34fb03c2b",
            "hw_version": "vmx-19",
            "instance_uuid": "5037caee-7c17-798a-8910-c8462d438d54",
            "ipv4": null,
            "ipv6": null,
            "module_hw": true,
            "moid": "vm-62",
            "snapshots": [],
            "tpm_info": {
                "provider_id": null,
                "tpm_present": false
            },
            "vimref": "vim.VirtualMachine:vm-62",
            "vnc": {}
        }
    }
}

PLAY RECAP ***************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible Community.VMware.TICSS]$

```

Ahora podemos continuar con los otros playbooks, con esta misma lógica...

# Funcion de cada Archivo en el proyecto

- ansible.cfg .- Contine las variables por defecto del proyecto, en este caso el ambiente Python 3.9
- inventory .- Contine los host que trabajaremos en el proyecto
- requirement.yml .- Contine las calecciones de Galaxy que usaremosen el proyecto
- vars.yml .- Contine las variables del proyecto --{falta incluir encripcion para passwrds*}
- create_vm.yml .- Playbook para crear una VM solo el HW son SO
- vm_deploy_template.yml .- Playbook para crea una VM usando un template
- vm_info.yml Playbook para obtener la información de una VM en especial
- vm_instalacion_licencias.yml .- Playbook para "planchar" lincencias en vSphere --{falta incluir dicionarios*}



Version: 2 - Isaac Torres