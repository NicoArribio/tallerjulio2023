<h1 align="center">Obligatorio Taller Instalación Servidores Linux</h1>

<h3 align="center"><img src="https://iili.io/HtXjYhB.md.png" alt="HtXjYhB.md.png" border="0"></a>


 
 <br>
 <br>
 <br>
 
 

### En este trabajo se tocaron los siguientes temas
- Primer contacto con Github.
- Instalacion y particionado de Discos
- Instalacion y configuracion de Servidores Rocky y Ubuntu para desplegar tareas de ansible.
- Agregar un usuario ansible que corra en los equipos sin pedir  contraseña.
- Armado de playbooks para realizar las siguientes tareas:
  <br>


------------


> Realizar la instalación de la aplicación Tomcat usada en el obligatorio de Administración de Servidores, dentro de un container en el servidor Rocky.

------------
> Configurar un servidor web apache como proxy reverso en el servidor Rocky. 

------------

> Instalar la base de datos mariadb en el servidor Ubuntu

------------

> Tener firewall activo habilitando los accesos necesarios en ambos servidores.

------------

> El playbook debe ser válido tanto para CentOS como para Ubuntu.

------------
### Entorno que debe tener configurado el ambiente para poder obtener un funcionamiento optimo.

```bash
Instalar dos servidores con 14GB de Disco, que tenga una partición de 1GB para /boot y el resto del disco en un volumen lógico de 6GB para /, 4GB para /var 2GB para swap.
Un servidor debe tener el SO. Rocky y el otro Ubuntu. 
Deben tener 2 interfaces de red, 1 conectada a NAT y la otra a una red Interna que le permita conectarse al equipo bastión con Ansible. 
Agregue un usuario ansible, darle permisos con SUDO sin contraseña. 
Desde el equipo bastión, copie la clave pública para poder conectarse al servidor sin contraseña.
todo esto teniendo en cuenta un ambiente en virtualbox ultima version.
```



### Primeros pasos

------------
> Configuramos nuestra cuenta en <https://github.com>
------------
> Realizamos un update a todos los equipos.
```bash
---
- hosts: all
  become: yes
  remote_user: ansible

  tasks:

  - name: Update all available packages for RedHat servers
    yum:
      name: "*"
      state: latest
    notify: Restart server
    when: ansible_os_family == "RedHat"

  - name: Update all available packages for Debian servers
    apt:
      name: "*"
      state: latest
      update_cache: yes
    notify: Restart server
    when: ansible_os_family == "Debian" 


  handlers:

  - name: Restart server
    reboot:       
```
------------

## AUTORES
Nicolas Arribio - 
Angel Brazionis


## Licencia

[MIT](https://choosealicense.com/licenses/mit/)
