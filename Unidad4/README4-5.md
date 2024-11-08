# Práctica 4.5 App Spring Boot

## Objetivo
Al finalizar esta práctica, serás capaz de desplegar una aplicación Spring Boot en K8s.


## Duración aproximada
40 minutos

## Instrucciones

### Paso 1. Configuración del espacio de nombres

Crea un **Namespace** para organizar y aislar los recursos asociados a esta práctica.

1. Crea una nueva directorio de trabajo en el nodo maestro, por ejemplo, **ws2**

2. Crea un archivo YAML llamado namespace.YAML

```yaml 
apiVersion: v1
kind: Namespace
metadata:
  name: springboot-app-ns
```

3. Aplica el YAML para crear el Namespace.

```bash
kubectl apply -f namespace.yaml
```

4. Verifica la creación del Namespace.

```bash
kubectl get namespaces
kubectl get namespace springboot-app-ns
kubectl describe namespace springboot-app-ns

```

<br/>

### Paso 2. Crear el ConfigMap

Define un **ConfigMap** para almacenar las variables de configuración de la aplicación.

1. Crea un archivo YAML llamado **congigmap.yaml**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: springboot-app-config
  namespace: springboot-app-ns
data:
  SPRING_DATASOURCE_URL: "jdbc:h2:mem:testdb"
  SPRING_DATASOURCE_USERNAME: "sa"
  SPRING_DATASOURCE_PASSWORD: ""
  DK_PARTICIPANTE: "nombre"
```

2. Aplica el archivo YAML para crear el **ConfigMap"**

```bash
kubectl apply -f configmap.yaml
```

3. Verifica la creación del **ConfigMap**

```bash
kubectl describe configmap springboot-app-config -n springboot-app-ns

# Detalles del ConfigMap

kubectl get configmap springboot-app-config -n springboot-app-ns -o yaml

```

<br/>

### Paso 3. Definir el Deployment con dos réplicas

El Deployment especificará que deseas tener dos réplicas de la aplicación, _distribuidas en dos Pods_.

1. Crea un archivo YAML llamado deployent.yaml

```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-app-deployment
  namespace: springboot-app-ns
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springboot-app
  template:
    metadata:
      labels:
        app: springboot-app
    spec:
      containers:
        - name: springboot-app
          image: <dockerhub-username>/springboot-app:latest  # Reemplaza con la URL de tu imagen en Docker Hub
          ports:
            - containerPort: 8080
          envFrom:
            - configMapRef:
                name: springboot-app-config

```

- **Nota**:  Reemplaza <dockerhub-username>/springboot-app:latest con la URL de tu imagen en Docker Hub. Por ejemmplo la imagen creada en la práctica 1.6

2. Aplica el archivo YAML para crear el **Deployment**

```bash
kubectl apply -f deployment.yaml
```

3. Verifica los detalles completos de un Deployment en Kubernetes

```bash
kubectl describe deployment <deployment-name> -n <namespace-name>
kubectl get deployment <deployment-name> -n <namespace-name> -o yaml
```


**Nota**:  Reemplaza `<deployment-name>` con el nombre de tu Deployment y `<namespace-name>` con el nombre del namespace donde se encuentra. 

<br/>

### Paso 4. Exponer el Deployment con un Service

Permitir el acceso a la aplicación desde dentro del clúster, crea un Service de tipo **ClusterIP**.

1. Crea un archivo YAML llamado `service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: springboot-app-service
  namespace: springboot-app-ns
spec:
  selector:
    app: springboot-app
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: ClusterIP
```

2. Aplica el archivo YAML para crear el Service.

```bash
kubectl apply -f service.yaml
```

3. Verificar el servicio creado

```bash
kubectl get svc -n springboot-app-ns
```

<br/>

### Paso 5. Verificar el despliegue

1. Asegúrate de que los Pods estén en ejecución:

```bash
kubectl get pods -n springboot-app-ns
```

2. Verifica que el servicio esté creado correctamente:

```bash
kubectl get svc -n springboot-app-ns
```

3. Valida los objetos creados en un Namespace específico, puedes utilizar el siguiente comando de Kubernetes

```bash
kubectl get all -n <namespace-name>
```

**Nota**: Reemplaza <namespace-name> por el nombre de tu namespace, por ejemplo, springboot-app-ns.

<br/>

### Paso 6. Consumir el servicio

Para consumir tu servicio con cur/wget desde dentro del clúster de Kubernetes, puedes usar la IP del Cluster (CLUSTER-IP) y el puerto expuesto (PORT) del servicio. En este caso (documentación de la práctica), el servicio `springboot-app-service` tiene la dirección IP **10.111.232.187** y expone el puerto **8095**.

<br/>

#### Opción A. Ejecutar el curl/wget dentro del clúster.

- Si ejecutas curl desde otro Pod en el mismo clúster, puedes hacer lo siguiente:


    ```bash
    curl http://10.111.232.187:8095
    ```

<br/>

#### Opción B. Usar el nombre del servicio en lugar de la IP

- En Kubernetes, los servicios pueden ser alcanzados por su nombre

   ```bash
    curl curl http://springboot-app-service:8095
   ```

<br/>

#### Opción C. port-forward para consumir desde tu máquina local


- Si deseas acceder al servicio desde tu máquina local, utiliza el comando **port-forward** para mapear el puerto del servicio en tu máquina:

```bash
kubectl port-forward svc/springboot-app-service 8095:8095 -n springboot-app-ns
```

- Luego, puedes consumir el servicio con curl/wget en tu máquina local:

```bash
wget http://localhost:8095
```

- Estas opciones te permitirán consumir el servicio springboot-app-service con curl según tu entorno de trabajo.

<br/>

### Paso 7. Limpieza

- Para limpiar todos los recursos de esta práctica en Kubernetes, eliminar el namespace en el que creaste los objetos es la forma más sencilla, ya que eso eliminará todos los recursos asociados dentro del mismo.  

```bash
# Eliminación del namespace
kubectl delete namespace springboot-app-ns

# Verificación
kubectl get namespaces
```

<br/><br/>
## Resultado Esperado

- Captura de pantalla que muestra el contenido del YAML para crear el espacio de nombes, la aplicación del YAML y vericación del mismo.

![kubectl](../images/u4_5_1.png)

<br/>

- Captura de pantalla que muestra el contenido del YAML para crear un ConfigMap, la aplicación del YAML y los detalles del ConfigMap después de crearlo.

![kubectl](../images/u4_5_2.png)

<br/>

- Captura de pantalla que muestra el contenido del YAML para crear un Deployment, la aplicación del YAML y verificación de la creación del mismo.

![kubectl](../images/u4_5_3.png)

<br/>

- Captura de pantalla que muestra los detalles del Deployment creado en el punto anterior.

![kubectl](../images/u4_5_4.png)

<br/>

- Captura de pantalla que muestra el contenido del YAML para crear el Service, la aplicación del YAML y la verificación del Servicio, nombre, IP y puerto del servicio.

![kubectl](../images/u4_5_5.png)

<br/>

- Captura de pantalla que muestra nuevamente la creación del servcio, así como la salida de `kubectl describe` del Service. 

![kubectl](../images/u4_5_6.png)

<br/>

- Captura de pantalla que muestra el contenido del JSON con las propiedades del objeto a insertar, la verificación de la cantidad y nombres de los Pods, la verificación de los detalles de conexión del servicio y el consumo, usando el comando **curl**

![kubectl](../images/u4_5_7.png)

<br/>

- Captura de pantalla que muestra el contenido JSON de un segundo objeto a insertar en el servicio y la verificación de los objetos insertados.

![kubectl](../images/u4_5_8.png)

<br/>

- Captura de pantalla que muestra las inconsistencias al tener una replica de ambos servicios, y al gestionar la base de datos en memoria. Observe como una misma petición se encuentra balanceada entre las replicas creadas y los datos en cada solicitud pueden ser diferentes.

![kubectl](../images/u4_5_9.png)

<br/>

- Captura de pantalla que muestra el consumo del servicio desde un Pod temporal, utilizando el comando **wget** y **springboot-app-service** en lugar de la IP.

![kubectl](../images/u4_5_10.png)

<br/>

- Captura de pantalla que muestra el consumo del servicio, usando la opción **port-forward**, observe como los consumos pueden realizarce usando _http://localhost_

![kubectl](../images/u4_5_11.png)

<br/>

- Captura de pantalla que muestra un listado de todos los YAMLs usados en esta práctica.

![kubectl](../images/u4_5_12.png)

<br/>

- Captura de pantalla que muestra la tarea de limpieza de los recursos creados en el namespace de la práctica

![kubectl](../images/u4_5_13.png)

<br/>
