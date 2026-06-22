# Guia de Conexion a la Terminal

Esta guia explica como conectarse a la terminal en distintos escenarios: local, Docker y remoto via SSH.

---

## 1. Terminal Local

Abre la terminal de tu sistema operativo:

- **Linux**: `Ctrl + Alt + T` o busca "Terminal" en el menu de aplicaciones.
- **macOS**: `Cmd + Space`, escribe `Terminal` y presiona Enter.
- **Windows**: Abre `PowerShell` o `Command Prompt` desde el menu Inicio, o usa `Windows Terminal`.

---

## 2. Conexion a un Contenedor Docker

Para conectarte a la terminal de un contenedor Docker en ejecucion:

```bash
# Listar contenedores activos
docker ps

# Conectarse al contenedor (reemplaza <container_id> con el ID o nombre del contenedor)
docker exec -it <container_id> /bin/bash

# Si bash no esta disponible, intenta sh
docker exec -it <container_id> /bin/sh
```

### Iniciar un contenedor con terminal interactiva

```bash
docker run -it <imagen> /bin/bash

# Ejemplo con una imagen de Python
docker run -it python:3.11 /bin/bash
```

### Adjuntarse a un contenedor en ejecucion

```bash
docker attach <container_id>
```

> **Nota**: Con `docker attach` compartes el proceso principal del contenedor. Usar `docker exec` es generalmente preferible para no interrumpir el proceso principal.

---

## 3. Conexion Remota via SSH

```bash
# Sintaxis basica
ssh usuario@direccion_ip

# Ejemplo
ssh admin@192.168.1.100

# Con puerto personalizado
ssh -p 2222 usuario@direccion_ip

# Con clave privada
ssh -i ~/.ssh/mi_clave.pem usuario@direccion_ip
```

### Configuracion rapida (`~/.ssh/config`)

Para no escribir todos los parametros cada vez, agrega una entrada en `~/.ssh/config`:

```
Host mi-servidor
    HostName 192.168.1.100
    User admin
    Port 2222
    IdentityFile ~/.ssh/mi_clave.pem
```

Luego conectate simplemente con:

```bash
ssh mi-servidor
```

---

## 4. Verificar que la Conexion esta Activa

```bash
# Ver las sesiones SSH activas
who

# Ver procesos de la terminal
ps aux | grep bash

# Ver informacion del sistema
uname -a
hostname
```

---

## 5. Salir de la Terminal / Cerrar Conexion

```bash
# Salir de la sesion
exit

# O con el atajo de teclado
Ctrl + D
```

---

## Referencias

- [Docker exec docs](https://docs.docker.com/reference/cli/docker/container/exec/)
- [OpenSSH manual](https://www.openssh.com/manual.html)
