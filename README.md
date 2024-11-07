
# RabbitMQ Ejemplos

Este proyecto contiene ejemplos de integración usando RabbitMQ para mostrar comunicaciones desacopladas entre procesos. A continuación, se describen los pasos para configurar RabbitMQ y ejecutar los ejemplos disponibles.

## Prerrequisitos

Para que los ejemplos funcionen, es necesario que RabbitMQ esté en ejecución en el puerto `5672`. Una forma simple de desplegar RabbitMQ localmente es a través de un contenedor Docker.

### Instalación de RabbitMQ con Docker

1. **Abrir una terminal**: En Windows, puedes utilizar PowerShell o el Símbolo del sistema.

2. **Ejecutar el siguiente comando** en la terminal para iniciar RabbitMQ:
   ```
   docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
   ```
   Este comando descargará la imagen de RabbitMQ (si no está disponible localmente) y la iniciará en los puertos:

    - `5672`: Para la comunicación de aplicaciones.
    - `15672`: Para la interfaz de administración web.

3. **Verificar que RabbitMQ está en ejecución**: Usa el comando siguiente para verificar los contenedores activos:
   ```
   docker ps
   ```
   Deberías ver el contenedor `rabbitmq` en ejecución.

4. **Acceso a la interfaz de administración**: Abre [http://localhost:15672](http://localhost:15672) en tu navegador e ingresa las credenciales:

    - **Usuario**: `guest`
    - **Contraseña**: `guest`

   Puedes encontrar más detalles sobre la imagen oficial de RabbitMQ en el siguiente [link](https://hub.docker.com/_/rabbitmq "link").

## Ejemplos incluidos en el proyecto

Este proyecto incluye dos ejemplos de uso de RabbitMQ:

1. **Simple Communication**: Muestra la integración desacoplada entre dos procesos. En este caso, debes:
    - Levantar primero el proceso receptor (`Recv`).
    - Luego, iniciar el proceso emisor para enviar mensajes.

2. **Worker Queues**: Ilustra cómo funcionan los "Workers" en RabbitMQ. Para ejecutar este ejemplo:
    - Levanta primero dos instancias del proceso "worker".
    - Luego, ejecuta el productor para enviar tareas a los workers.

## Ejecución del Proceso Receptor

Para ejecutar el proceso receptor, asegúrate de que RabbitMQ está en ejecución y configurado correctamente en `localhost:5672`. Puedes ejecutar la clase `Recv` incluida en el proyecto, la cual se conectará a RabbitMQ y esperará mensajes en la cola configurada.

## Notas adicionales

- La interfaz de administración de RabbitMQ permite monitorear colas, verificar mensajes y ver el estado de las conexiones activas.
- Si deseas detener RabbitMQ, ejecuta:
   ```
   docker stop rabbitmq
   ```
- Para reiniciar el contenedor detenido, usa:
   ```
   docker start rabbitmq
   ```

Con estos pasos, deberías tener un entorno listo para ejecutar los ejemplos de comunicación con RabbitMQ.