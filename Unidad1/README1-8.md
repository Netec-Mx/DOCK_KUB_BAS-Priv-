# Práctica 1.8 Docker CLI (Opcional)

## Objetivo

Al finalizar esta actividad, serás capaz de optimizar un Dockerfile aplicando prácticas recomendadas para reducir el tamaño de la imagen, mejorar la velocidad de construcción y minimizar el uso de recursos.


## Duración aproximada

20 minutos

## Instrucciones

### 1. Preparación Inicial
   - Abre una terminal y asegúrate de que Docker esté en funcionamiento.
   - Verifica la versión de Docker:
     ```bash
     docker --version
     ```

### 2. Descarga de Imágenes de Docker Hub
   - Descarga las siguientes imágenes adicionales para familiarizarte con diferentes sistemas y aplicaciones:
     - `redis`: Sistema de base de datos en memoria.
     - `mysql`: Sistema de gestión de bases de datos.
     - `node`: Imagen base para aplicaciones Node.js.
     - `python`: Imagen base para aplicaciones Python.

   - Ejemplo de comando para cada imagen:
     ```bash
     docker pull redis
     docker pull mysql
     docker pull node
     docker pull python
     ```

### 3. Construcción de Contenedores
   - Crea un contenedor a partir de cada imagen descargada:
     - **Redis**:
       ```bash
       docker run -d --name redis_container redis
       ```
     - **MySQL**:
       ```bash
       docker run -d --name mysql_container -e MYSQL_ROOT_PASSWORD=abcd12345 mysql
       ```
     - **Node**:
       ```bash
       docker run -d --name node_container node tail -f /dev/null
       ```
     - **Python**:
       ```bash
       docker run -d --name python_container python tail -f /dev/null
       ```
   - Ahora tendrás varios contenedores corriendo simultáneamente, cada uno asociado con un sistema o aplicación diferente.

### 4. Visualización de Imágenes y Contenedores
   - Lista todas las imágenes disponibles en tu sistema:
     ```bash
     docker images
     ```
   - Lista todos los contenedores, tanto activos como detenidos:
     ```bash
     docker ps -a
     ```

### 5. Inspección Detallada
   - **Puertos HTTP expuestos**: Confirma qué contenedores exponen puertos HTTP:
     ```bash
     docker port nginx_container
     docker port httpd_container
     ```
   - **Sistema Operativo**: Inspecciona el sistema operativo de cada contenedor:
     ```bash
     docker inspect <nombre_del_contenedor> | grep "Os"
     ```
   - **Fecha y Hora**: Muestra la fecha y hora actual en uno de los contenedores:
     ```bash
     docker exec redis_container date
     ```

### 6. Eliminación de Contenedores e Imágenes
   - **Detener y eliminar todos los contenedores**:
     ```bash
     docker stop $(docker ps -aq)
     docker rm $(docker ps -aq)
     ```
   - **Eliminar todas las imágenes**:
     ```bash
     docker rmi $(docker images -q)
     ```

### 7. Reflexión sobre el Docker Daemon y el CLI
   - Reflexiona sobre cómo la separación entre el Docker Daemon y el cliente CLI permite gestionar contenedores en otros servidores desde una máquina local.


---

## Preguntas al Finalizar la Práctica

1. ¿Cuántas imágenes Docker se generaron?
2. ¿Cuántos contenedores Docker existen al finalizar la práctica?
3. ¿Cuáles son los puertos HTTP expuestos?
4. ¿Qué sistema operativo tiene cada contenedor creado en esta práctica?
5. ¿Cuál es la fecha y hora reportada en uno de los contenedores en ejecución?
6. Explica cómo la separación entre el Docker Daemon y el cliente CLI permite la interacción con contenedores en otros servidores.

---

## Resultado Esperado

- Imágenes Docker

![docker images](../images/u1_8_1.png)

- Contenedores Docker

![docker ps -a](../images/u1_8_2.png)