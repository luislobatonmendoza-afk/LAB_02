# Laboratorio 02: Docker Compose - Luis Lobaton

Proyecto configurado con varios contenedores utilizando Docker Compose, integrando una API de Node.js en tres réplicas junto con una base de datos PostgreSQL persistente.

## Teoría de Volúmenes y Redes en Docker

### Volúmenes (Volumes)
Los volúmenes son un mecanismo el cual es el preferido por Docker para persistir los datos generados y utilizados por los contenedores. 
- **Persistencia**: A diferencia del sistema de archivos de un contenedor, que se borra al destruir el contenedor, un volumen se almacena fuera del ciclo de vida de este en el host.
- **Caso de uso en este laboratorio**: En la actividad lo usamos en el servicio de PostgreSQL (`pgdata`) para garantizar que la información de la base de datos no se pierda si reiniciamos o apagamos los contenedores.

### Redes (Networks)
Docker Compose crea automáticamente una red bridge predeterminada para cada proyecto. 
- **Comunicación interna**: Todos los servicios definidos en el archivo `docker-compose.yaml` pueden comunicarse entre ellos utilizando el nombre del servicio como hostname.
- **Aislamiento**: Permite que los contenedores interactúen de forma segura dentro de la misma red virtual sin exponer puertos innecesarios al exterior, manteniendo pública únicamente la puerta de enlace mapeada, como los puertos `3001`, `3002`, `3003` para las réplicas de la API y el `5432` para la base de datos.

### Créditos
 Lobaton Mendoza Luis Angel Manuel