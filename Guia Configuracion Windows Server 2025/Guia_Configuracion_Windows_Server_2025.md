# Guía de configuración inicial de Windows Server 2025

> **Objetivo:** realizar la configuración básica de un servidor Windows
> Server 2025 después de su instalación y dejarlo preparado para las
> tareas posteriores de red, dominio y Active Directory.


> **Importante:** el apartado de **Active Directory** se realizará
> posteriormente en una guía independiente.

------------------------------------------------------------------------

# 1. Conocer el Administrador del servidor

Después de iniciar sesión en Windows Server 2025 con una cuenta
administrativa, normalmente se abre automáticamente el **Administrador
del servidor (Server Manager)**. Es la consola principal desde la que
vamos a administrar el servidor y acceder a muchas de sus herramientas.

Microsoft indica que Server Manager permite administrar el servidor local
y también otros servidores Windows que se hayan añadido a la consola.
Desde aquí podemos consultar el estado del servidor, instalar o quitar
roles y características, acceder a herramientas administrativas y
realizar tareas de configuración. citeturn0search0turn0search1

📸 **CAPTURA 01 --- Ventana principal del Administrador del servidor**

## 1.1. ¿Qué vemos al abrirlo?

La ventana se puede entender en tres zonas principales:

1. **Barra superior:** contiene los menús y controles generales.
2. **Panel de navegación izquierdo:** permite cambiar entre las
   diferentes vistas de administración.
3. **Zona central:** muestra la información y las tareas disponibles
   para la vista seleccionada.                                                                  

------------------------------------------------------------------------

## 1.2. Panel de navegación izquierdo

En una instalación inicial encontraremos principalmente:

### Panel

Es la pantalla inicial del Administrador del servidor.

Aquí se muestra una visión general del estado del servidor y se
organizan diferentes bloques de información. Es la vista que utilizaremos
para tener una primera visión de conjunto.

### Servidor local

Muestra información y propiedades del propio servidor que estamos
administrando.

Desde esta sección podremos comprobar o modificar, entre otros:

- Nombre del equipo.
- Grupo de trabajo o dominio.
- Dirección y configuración de red.
- Windows Update.
- Administración remota.
- Firewall.
- Escritorio remoto.
- Zona horaria.
- Estado de activación.

Además, la página del servidor local puede mostrar información sobre
eventos, servicios, rendimiento y resultados del **Best Practices
Analyzer (BPA)**. citeturn0search0

📸 **CAPTURA 02 --- Panel de navegación y opción Servidor local**

### Todos los servidores

Esta vista permite trabajar con los servidores que forman parte del
grupo de servidores administrados por Server Manager.

En nuestra práctica inicial tendremos principalmente nuestro propio
servidor. Más adelante, cuando trabajemos con una infraestructura con
varios equipos, esta sección será especialmente útil.

### Páginas de roles

Cuando instalemos determinados **roles** y Server Manager los detecte,
pueden aparecer nuevas páginas en el panel de navegación.

Por ejemplo, después de instalar un rol de servidor, podremos encontrar
una sección específica desde la que consultar su estado y acceder a
tareas relacionadas con ese rol. citeturn0search0

> **Todavía no vamos a instalar Active Directory.** Primero dejaremos
> correctamente configurado el servidor.

------------------------------------------------------------------------

## 1.3. Menú Administrar

El menú **Administrar** contiene acciones generales de administración.

Entre las opciones más importantes encontraremos:

- **Agregar roles y características:** permite instalar nuevos roles y
  características en el servidor.
- **Quitar roles y características:** permite eliminar roles o
  características instalados.
- **Agregar servidores:** permite incorporar otros servidores a la
  consola de Server Manager.
- **Crear grupo de servidores:** permite organizar servidores en grupos
  personalizados.
- **Propiedades del Administrador del servidor:** permite configurar
  aspectos del funcionamiento de la propia consola.

Para nuestra práctica, una de las opciones más importantes será
**Agregar roles y características**, que utilizaremos más adelante para
instalar los servicios que necesitemos. citeturn0search5

📸 **CAPTURA 03 --- Menú Administrar desplegado**

------------------------------------------------------------------------

## 1.4. Menú Herramientas

El menú **Herramientas** da acceso a numerosas herramientas
administrativas de Windows Server.

Algunas de las que utilizaremos durante el curso son:

- **PowerShell**
- **Visor de eventos**
- **Servicios**
- **Administración de equipos**
- **Administración de discos**
- **Firewall de Windows Defender con seguridad avanzada**
- Herramientas relacionadas con los roles instalados.

Server Manager utiliza este menú para proporcionar accesos a
herramientas administrativas y complementos MMC disponibles en el
sistema. citeturn0search0

📸 **CAPTURA 04 --- Menú Herramientas desplegado**

> **Idea importante:** cuando en una práctica te indiquemos
> **Administrador del servidor → Herramientas → ...**, estamos utilizando
> este menú para abrir una herramienta concreta de administración.

------------------------------------------------------------------------

## 1.5. Menú Ver

El menú **Ver** permite modificar la forma en la que visualizamos la
consola.

Entre otras opciones permite controlar el zoom y actualizar la
información mostrada. La tecla **F5** permite actualizar la vista. citeturn0search0turn0search9

📸 **CAPTURA 05 --- Menú Ver desplegado**

------------------------------------------------------------------------

## 1.6. Menú Ayuda

El menú **Ayuda** permite acceder a la ayuda y documentación relacionada
con Server Manager.

También podemos utilizar **F1** para abrir la ayuda de Server Manager.
citeturn0search9

📸 **CAPTURA 06 --- Menú Ayuda desplegado**

------------------------------------------------------------------------

## 1.7. ¿Qué vamos a utilizar de momento?

Para esta primera configuración nos interesa especialmente conocer:

```text
ADMINISTRADOR DEL SERVIDOR
        │
        ├── Panel
        │     └── Vista general del servidor
        │
        ├── Servidor local
        │     └── Configuración básica
        │
        ├── Todos los servidores
        │     └── Administración de varios servidores
        │
        ├── Administrar
        │     └── Roles, características y configuración de Server Manager
        │
        └── Herramientas
              └── PowerShell, eventos, discos, firewall, servicios...
```

La idea es que, antes de comenzar a modificar el servidor, seas capaz de
responder:

- ¿Dónde puedo comprobar el nombre del servidor?
- ¿Dónde puedo revisar la configuración de red?
- ¿Dónde puedo instalar un rol?
- ¿Dónde puedo abrir PowerShell?
- ¿Dónde puedo consultar los eventos?
- ¿Dónde puedo administrar los discos?
- ¿Dónde puedo abrir el firewall avanzado?

📸 **CAPTURA 07 --- Vista general del Administrador del servidor**

------------------------------------------------------------------------
## 2. Datos iniciales del servidor

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
> red. Los siguientes son únicamente un ejemplo.

  Parámetro          Ejemplo
  ------------------ ----------------------------------------
  IPv4               `192.168.100.10`
  Máscara            `255.255.255.0`
  Puerta de enlace   `192.168.100.1`
  DNS preferido      Según la configuración de la red

### Pasos

1.  Abrir las propiedades del adaptador de red.
2.  Seleccionar **Protocolo de Internet versión 4 (TCP/IPv4)**.
3.  Seleccionar **Usar la siguiente dirección IP**.
4.  Introducir los valores correspondientes.
5.  Configurar el DNS según el diseño de la red.
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

# 19. Resolución de problemas

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

A partir de aquí comenzará la configuración de Active Directory y del
dominio.

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
