# Guía de configuración inicial de Windows Server 2025

> **Objetivo:** realizar la configuración básica de un servidor Windows
> Server 2025 después de su instalación y dejarlo preparado para las
> tareas posteriores de red, dominio y Active Directory.


> **Importante:** el apartado de **Active Directory** se realizará
> posteriormente en una guía independiente.

------------------------------------------------------------------------

## 1. Antes de empezar

Anota los datos que vas a utilizar en tu práctica.

| Dato                  |                                    Valor |
| ------------------    | ---------------------------------------: |
| Nombre del servidor   |                           `SRV-WIN2025`  |
| Sistema operativo     |                      Windows Server 2025 |
| Usuario administrador |                       `Administrador`    |
| Dirección IPv4        |                                          |
| Máscara de red        |                                          |
| Puerta de enlace      |                                          |
| Servidor DNS          |                                          |
| Dominio               |            Se configurará posteriormente |

 

                   

📸 **CAPTURA 01 --- Datos iniciales del servidor**

------------------------------------------------------------------------

# 2. Administrador del servidor

El **Administrador del servidor (Server Manager)** es la herramienta
principal para realizar muchas tareas de administración de Windows
Server. Permite consultar el estado del servidor, administrar roles y
características y acceder a herramientas de configuración.

### 2.1. Abrir el Administrador del servidor

Normalmente se abre automáticamente después de iniciar sesión.

También podemos abrirlo desde:

**Inicio → Administrador del servidor**

Otra posibilidad es ejecutar:

``` text
ServerManager.exe
```

📸 **CAPTURA 02 --- Administrador del servidor**

### 2.2. Propiedades del Administrador del servidor

Desde:

**Administrar → Propiedades del Administrador del servidor**

podemos configurar, entre otras cosas, si queremos que se abra
automáticamente al iniciar sesión y el intervalo de actualización.

📸 **CAPTURA 03 --- Propiedades del Administrador del servidor**

------------------------------------------------------------------------

# 3. Configurar este servidor local

En el Administrador del servidor seleccionamos:

**Servidor local**

Aquí podemos consultar y modificar propiedades importantes:

-   Nombre del equipo.
-   Grupo de trabajo o dominio.
-   Configuración de red.
-   Actualizaciones.
-   Firewall.
-   Administración remota.
-   Escritorio remoto.
-   Zona horaria.
-   Activación.

📸 **CAPTURA 04 --- Servidor local**

------------------------------------------------------------------------

# 4. Configurar fecha, hora y zona horaria

Es importante que el servidor tenga correctamente configuradas la fecha,
la hora y la zona horaria. Esto será especialmente importante cuando
posteriormente trabajemos con **dominios y Active Directory**, donde la
sincronización horaria es relevante.

### Pasos

1.  Abrir la configuración de **fecha y hora**.
2.  Comprobar la zona horaria.
3.  Comprobar fecha y hora.
4.  Comprobar la sincronización horaria.
5.  Aplicar los cambios si fueran necesarios.

📸 **CAPTURA 05 --- Configuración de fecha y hora**

### Comprobación con PowerShell

``` powershell
Get-Date
```

📸 **CAPTURA 06 --- Comprobación con PowerShell**

------------------------------------------------------------------------

# 5. Cambiar el nombre del servidor

El nombre del equipo permite identificar el servidor dentro de la red.

Para esta práctica utilizaremos como ejemplo:

``` text
SRV-WIN2025
```

### 5.1. Cambiar el nombre

Desde:

**Administrador del servidor → Servidor local → Nombre del equipo**

también podemos acceder a:

**Configuración → Sistema → Acerca de → Cambiar nombre de este equipo**

Escribe:

``` text
SRV-WIN2025
```

Confirma el cambio.

📸 **CAPTURA 07 --- Ventana para cambiar el nombre**

📸 **CAPTURA 08 --- Nuevo nombre del servidor**

### 5.2. Reiniciar y comprobar

Reinicia el servidor para aplicar el cambio.                                                  Después comprueba:

``` powershell
hostname
```

También:

``` powershell
$env:COMPUTERNAME
```

📸 **CAPTURA 09 --- Comprobación del nombre del servidor**

------------------------------------------------------------------------

# 6. Configurar la red

La configuración de red es una de las tareas más importantes antes de
continuar con la administración del servidor.

### 6.1. Comprobar la configuración actual

Abre PowerShell y ejecuta:

``` powershell
ipconfig
```

Para obtener información detallada:

``` powershell
ipconfig /all
```

Identifica:

-   Dirección IPv4.
-   Máscara de subred.
-   Puerta de enlace.
-   Servidores DNS.
-   Adaptador de red utilizado.

📸 **CAPTURA 10 --- Configuración de red con ipconfig /all**

------------------------------------------------------------------------

# 7. Configurar una dirección IPv4 estática

Para un servidor que posteriormente ofrecerá servicios de red y
funciones de dominio, es conveniente trabajar con una dirección IP
estable.

> **Importante:** utiliza los valores de red indicados para tu
> laboratorio. Los siguientes son únicamente un ejemplo.

  Parámetro          Ejemplo
  ------------------ ----------------------------------------
  IPv4               `192.168.100.10`
  Máscara            `255.255.255.0`
  Puerta de enlace   `192.168.100.1`
  DNS preferido      Según la configuración del laboratorio

### Pasos

1.  Abrir las propiedades del adaptador de red.
2.  Seleccionar **Protocolo de Internet versión 4 (TCP/IPv4)**.
3.  Seleccionar **Usar la siguiente dirección IP**.
4.  Introducir los valores correspondientes.
5.  Configurar el DNS según el diseño del laboratorio.
6.  Aceptar los cambios.

📸 **CAPTURA 11 --- Propiedades del adaptador de red**

📸 **CAPTURA 12 --- Configuración IPv4**

### 7.1. Comprobar la configuración

``` powershell
ipconfig /all
```

📸 **CAPTURA 13 --- IPv4 configurada**

------------------------------------------------------------------------

# 8. Comprobar la conectividad de red

## 8.1. Probar la propia máquina

``` powershell
ping 127.0.0.1
```

También:

``` powershell
ping DIRECCION_IP_DEL_SERVIDOR
```

📸 **CAPTURA 14 --- Ping al propio servidor**

## 8.2. Probar desde otro equipo

Desde el equipo cliente:

``` text
ping DIRECCION_IP_DEL_SERVIDOR
```

📸 **CAPTURA 15 --- Ping desde el equipo cliente al servidor**

## 8.3. Comprobar con PowerShell

``` powershell
Test-NetConnection DIRECCION_IP
```

Por ejemplo:

``` powershell
Test-NetConnection 192.168.100.10
```

📸 **CAPTURA 16 --- Test-NetConnection**

------------------------------------------------------------------------

# 9. Permitir las peticiones ping en el Firewall

Si el servidor está correctamente configurado pero no responde a `ping`,
puede que el firewall esté bloqueando las peticiones ICMP.

Abre:

**Administrador del servidor → Herramientas → Firewall de Windows
Defender con seguridad avanzada**

Selecciona:

**Reglas de entrada**

Busca:

**Archivos e impresoras compartidos (petición eco: ICMPv4 de entrada)**

Habilita la regla necesaria para las pruebas de laboratorio.


📸 **CAPTURA 17 --- Firewall de Windows con seguridad avanzada**

📸 **CAPTURA 18 --- Regla ICMPv4 de entrada**

📸 **CAPTURA 19 --- Regla ICMPv4 habilitada**

> **Nota:** no desactives el firewall completo para solucionar un
> problema de conectividad. Es preferible habilitar únicamente la regla
> necesaria.

------------------------------------------------------------------------

# 10. Administración remota

Windows Server permite administrar el servidor desde otro equipo.

Desde las propiedades del servidor podemos comprobar la configuración de
**Administración remota**.

Configúrala según las necesidades del laboratorio.

📸 **CAPTURA 23 --- Administración remota**

------------------------------------------------------------------------

# 11. Comprobar el Firewall

El firewall debe permanecer activo.

Podemos consultar su estado desde la configuración de seguridad o
mediante PowerShell:

``` powershell
Get-NetFirewallProfile
```

📸 **CAPTURA 24 --- Estado del Firewall**

------------------------------------------------------------------------

# 12. Herramientas de configuración: SConfig

Windows Server incluye herramientas para realizar tareas de
configuración desde la línea de comandos.

Ejecuta:

``` powershell
sconfig
```

Desde SConfig podemos realizar diferentes tareas de configuración del
servidor.

📸 **CAPTURA 25 --- SConfig**

> Algunas opciones pueden variar según la versión instalada y según si
> utilizamos Server Core o Desktop Experience.

------------------------------------------------------------------------

# 13. PowerShell

PowerShell es una herramienta fundamental para la administración de
Windows Server.

### 13.1. Nombre del equipo

``` powershell
hostname
```

o:

``` powershell
$env:COMPUTERNAME
```

📸 **CAPTURA 26 --- hostname**

### 13.2. Configuración de red

``` powershell
ipconfig
```

o:

``` powershell
ipconfig /all
```

📸 **CAPTURA 27 --- ipconfig**

### 13.3. Conectividad

``` powershell
ping DIRECCION_IP
```

y:

``` powershell
Test-NetConnection DIRECCION_IP
```

📸 **CAPTURA 28 --- Comprobación de conectividad**

------------------------------------------------------------------------

# 14. Comprobar el estado de los discos

## 14.1. CHKDSK

Para analizar una unidad:

``` cmd
chkdsk C:
```

Para comprobar y reparar cuando corresponda:

``` cmd
chkdsk C: /f
```

> El uso de `/f` puede requerir que la comprobación se realice durante
> el siguiente reinicio si la unidad está en uso.

📸 **CAPTURA 29 --- Comprobación con CHKDSK**

## 14.2. Comprobar archivos del sistema

``` cmd
sfc /verifyonly
```

También podemos utilizar:

``` cmd
sfc /scannow
```

📸 **CAPTURA 30 --- Comprobación SFC**

## 14.3. Repair-Volume

En PowerShell:

``` powershell
Repair-Volume -DriveLetter C -Scan
```

📸 **CAPTURA 31 --- Repair-Volume**

------------------------------------------------------------------------

# 15. Herramientas administrativas

Desde:

**Administrador del servidor → Herramientas**

podemos acceder a numerosas herramientas administrativas, entre ellas:

-   Servicios.
-   Administración de equipos.
-   Administración de discos.
-   Visor de eventos.
-   Firewall.
-   Administración de usuarios.
-   Administración de almacenamiento.

📸 **CAPTURA 32 --- Menú Herramientas**

------------------------------------------------------------------------

# 16. Consola de administración de Microsoft (MMC)

Windows incluye la **Microsoft Management Console (MMC)**.

Podemos ejecutar:

``` text
mmc
```

Los archivos `.msc` permiten acceder a diferentes consolas.

Ejemplos:

``` text
services.msc
eventvwr.msc
compmgmt.msc
diskmgmt.msc
wf.msc
```

📸 **CAPTURA 33 --- Consola MMC**

------------------------------------------------------------------------

# 17. Visor de eventos

El **Visor de eventos** permite consultar los registros generados por
Windows y resulta especialmente útil para localizar errores.

Podemos abrirlo mediante:

``` text
eventvwr.msc
```

Debemos conocer especialmente:

-   Aplicación.
-   Seguridad.
-   Sistema.

📸 **CAPTURA 34 --- Visor de eventos**

------------------------------------------------------------------------

# 18. Administración de discos

Podemos abrir la herramienta mediante:

``` text
diskmgmt.msc
```

Desde ella podemos consultar:

-   Discos instalados.
-   Particiones.
-   Volúmenes.
-   Espacio disponible.
-   Letras de unidad.
-   Estado de los discos.

📸 **CAPTURA 35 --- Administración de discos**

> **Precaución:** no elimines, formatees ni modifiques particiones sin
> comprobar previamente qué disco o volumen estás utilizando.

------------------------------------------------------------------------

# 19. Comprobación final

Antes de continuar con la siguiente parte, comprueba:

-   [ ] El servidor tiene un nombre adecuado.
-   [ ] Se ha reiniciado después de cambiar el nombre.
-   [ ] La fecha y hora son correctas.
-   [ ] La zona horaria es correcta.
-   [ ] La configuración IPv4 es correcta.
-   [ ] La dirección IP es la prevista para la práctica.
-   [ ] La configuración DNS es la prevista.
-   [ ] El servidor tiene conectividad con la red.
-   [ ] El servidor puede comunicarse con el equipo cliente.
-   [ ] El firewall está activo.
-   [ ] Las reglas necesarias para las pruebas de conectividad están
    configuradas.
-   [ ] Windows Update ha sido comprobado.
-   [ ] El estado de activación ha sido comprobado.
-   [ ] Se ha verificado el nombre con `hostname`.
-   [ ] Se ha comprobado la red con `ipconfig /all`.
-   [ ] Se ha comprobado la conectividad con `ping` o
    `Test-NetConnection`.
-   [ ] Se ha comprobado el estado básico de los discos.

📸 **CAPTURA 36 --- Estado final del servidor**

------------------------------------------------------------------------

# 20. Evidencias que debes entregar

Conserva las capturas que demuestren las principales configuraciones
realizadas:

1.  Administrador del servidor.
2.  Nombre del servidor.
3.  Fecha y hora.
4.  Configuración IPv4.
5.  `ipconfig /all`.
6.  Conectividad mediante `ping`.
7.  Regla ICMP del firewall.
8.  Windows Update.
9.  Estado del firewall.
10. `hostname`.
11. SConfig.
12. Herramientas administrativas.
13. Visor de eventos.
14. Administración de discos.
15. Comprobaciones de disco.

> Las capturas deben mostrar tanto la configuración realizada como,
> cuando sea posible, el resultado de la comprobación.

------------------------------------------------------------------------

# 21. Resolución de problemas

## El servidor no responde al ping

Comprueba:

1.  Que ambos equipos están en la misma red.
2.  Que las direcciones IP son correctas.
3.  Que la máscara de red es correcta.
4.  Que el adaptador de red está conectado.
5.  Que el firewall permite las peticiones ICMP necesarias.
6.  Que no existe otra configuración de red interfiriendo.

Puedes consultar:

``` powershell
ipconfig /all
```

y:

``` powershell
Test-NetConnection DIRECCION_IP
```

## No tengo conexión de red

Comprueba:

``` powershell
ipconfig /all
```

Después prueba la puerta de enlace:

``` powershell
ping DIRECCION_IP_PUERTA_ENLACE
```

Si la red funciona pero no se resuelven nombres, comprueba la
configuración DNS.

## He cambiado el nombre y no aparece

Comprueba:

``` powershell
hostname
```

Si el cambio todavía no aparece, reinicia el servidor.

## Windows Update no funciona

Comprueba:

-   Conectividad de red.
-   Fecha y hora.
-   Configuración DNS.
-   Estado de los servicios relacionados con Windows Update.
-   Posibles actualizaciones pendientes de reinicio.

------------------------------------------------------------------------

# 22. Preparación para la siguiente parte

Una vez terminada esta configuración inicial, el servidor estará
preparado para continuar con las tareas de administración de red.

``` text
CONFIGURACIÓN INICIAL
        │
        ▼
CONFIGURACIÓN DE RED
        │
        ▼
COMPROBACIÓN DE CONECTIVIDAD
        │
        ▼
INSTALACIÓN DE ROLES
        │
        ▼
ACTIVE DIRECTORY
        │
        ├── Usuarios
        ├── Grupos
        ├── Unidades organizativas
        ├── Equipos
        └── Directivas
```

> **No realices todavía la instalación y configuración de Active
> Directory. Ese contenido se trabajará en el siguiente apartado.**

------------------------------------------------------------------------

# 23. Resumen

Al finalizar esta guía debes tener un **Windows Server 2025
correctamente identificado, actualizado y conectado a la red**, con las
principales herramientas de administración local conocidas.

Debes ser capaz de:

-   Identificar el Administrador del servidor.
-   Configurar el nombre del equipo.
-   Configurar la fecha y hora.
-   Configurar IPv4.
-   Comprobar la conectividad.
-   Comprender el papel del firewall.
-   Utilizar `ping`.
-   Utilizar `ipconfig`.
-   Utilizar `Test-NetConnection`.
-   Utilizar SConfig.
-   Utilizar PowerShell.
-   Consultar eventos.
-   Administrar discos.
-   Realizar comprobaciones básicas del sistema.

**A partir de aquí comenzará la configuración de Active Directory y del
dominio.**
