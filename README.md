# Laboratorio 02: Docker Compose - Luis Lobaton

Proyecto configurado con varios contenedores utilizando Docker Compose, integrando una API de Node.js en tres réplicas junto con una base de datos PostgreSQL persistente.

## Teoría de Volúmenes y Redes en Docker

### Volúmenes (Volumes)
Los volúmenes son un mecanismo el cual es el preferido por Docker para persistir los datos generados y utilizados por los contenedores. 
- **Persistencia**: A diferencia del sistema de archivos de un contenedor, que se borra al destruir el contenedor, un volumen se almacena fuera del ciclo de vida de este en el host.
- **Caso de uso en este laboratorio**: En la actividad lo usamos en el servicio de PostgreSQL (`pgdata`) para garantizar que la información de la base de datos no se pierda si reiniciamos o apagamos los contenedores.

#### Tipos de Volúmenes en Docker:
**Volumes (Volúmenes gestionados):** Son administrados enteramente por Docker en una zona específica del host y es la opción recomendada para la persistencia de datos.
**Bind Mounts (Montajes de enlace):** Permiten mapear un archivo o directorio de la máquina anfitriona directamente dentro del contenedor.
**Tmpfs (Montajes temporales):** Los datos se almacenan únicamente en la memoria RAM del host y nunca se escriben en el disco físico.

### Redes (Networks)
Docker Compose crea automáticamente una red bridge predeterminada para cada proyecto. 
- **Comunicación interna**: Todos los servicios definidos en el archivo `docker-compose.yaml` pueden comunicarse entre ellos utilizando el nombre del servicio como hostname.
- **Aislamiento**: Permite que los contenedores interactúen de forma segura dentro de la misma red virtual sin exponer puertos innecesarios al exterior, manteniendo pública únicamente la puerta de enlace mapeada, como los puertos `3001`, `3002`, `3003` para las réplicas de la API y el `5432` para la base de datos.

#### Tipos de Redes en Docker:
**Bridge:** Red predeterminada al instalar Docker. Permite que los contenedores en la misma red se comuniquen entre sí aislados de otros.
**Host:** Elimina el aislamiento de red; el contenedor utiliza directamente la pila de red del host.
**Overlay:** Conecta múltiples daemons de Docker permitiendo comunicación entre nodos de un cluster (ej. Docker Swarm).
**Macvlan:** Permite asignar una dirección MAC a un contenedor para que aparezca como un dispositivo físico más en la red local.
**None:** Desactiva completamente la red para el contenedor (aislamiento total).

## Comandos para Despliegue

Para levantar todo el entorno de contenedores en segundo plano:
```bash
docker compose up -d
```

### Créditos
 Lobaton Mendoza Luis Angel Manuel