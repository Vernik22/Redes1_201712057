# Proyecto2_201712057

- Nombre: Vernik Carlos Alexander Yaxon Ortiz
- Carnet: 201712057

## Resumen de direcciones IP y VLAN

### VLAN
Para la creacion del Proyecto 1 se utilizaron las siguientes IDs para identificar a las Vlans de la topologia:

| VLAN   | ID | IP |
|----------|-----|----:|
| PLANEACION     |  17  | 192.168.17.254 /24  |
| FINANZAS |  27  | 192.168.27.254 /24  | 
| RRHH |  37  | 192.168.37.254 /24  |
| IT |  47  | 192.168.47.254 /24  |

### IPs Vpcs
Para la asignacion de IPs para las Vpc que se utilizaron, se iniciaron desde el 1 hasta el numero consecutivo siguiente.
Es decir que para las Vpcs qe se encuentran bajo la Vlan de "PLANEACION" se inicio con la configuracion desde la 192.168.17.1 ...

## Implementacion de la Topologia

### Datacenter

![D](./img/Datacenter.png)

### Backbone

![D](./img/Backbone.png)

### Area de Trabajo

![D](./img/Area_trabajo.png)

### Topologia Completa

![D](./img/Topologia.png)

## Comandos Utilizados

### Configuracion de VTP para Servidor

Debemos asignar el modo troncal a las interfaces necesarias.

```
configure terminal
interface range e0/1-2
switchport trunk encapsulation dot1q
switchport mode trunk
```

Luego debemos crear las Vlan con los siguientes comandos podremos crear todas las que necesitemos en este caso creamos 4

```
configure terminal
vlan 17
name PRIMERA
vlan 27
name SEGUNDA
end
```

Procegimos con la configuracion del server vtp simpre recordando escribir el comando "do write" para guardar nuestras configuraciones realizadas

```
configure terminal
vtp version 2
vtp mode server
vtp domain dominio
vtp password contrasena
do write
```

### Configuracion de VTP para Cliente

Procedemos a configurar las interfaces en modo troncal para el cliente.
```
configure terminal
interface e0/1
switchport trunk encapsulation dot1q
switchport mode trunk
```

Configuramos el modo cliente en el switch

```
configure terminal
vtp mode client
vtp domain dominio
vtp password contrasena
do write
```

Y por ultimo asignamos el modo de acceso a las Vlans que necesitemos.

```
configure terminal
interface e0/2
switchport mode access
switchport access vlan 17
interface e0/3
switchport mode access
switchport access vlan 27
do write
```

### Configuracion de Modo Transparente

Y por ultimo configuramos el modo transparente para el switch en el proyecto

```
configure terminal
vtp mode transparent
vtp domain dominio
vtp password contrasena
do write
```

## Pings entre Hosts

### Ping de Server RRHH hacia RRHH_1

![D](./img/Ping_ServerRRHH_RRHH_1.png)

### Ping de Server Planeacion hacia Planeacion_1

![D](./img/Ping_ServerPlaneacion_Planeacion1.png)
