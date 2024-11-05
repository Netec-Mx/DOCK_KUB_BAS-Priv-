# Práctica 2.2 Verificación de Instalación del Worker Node  

## Objetivo
Al finalizar esta actividad, serás capaz de verificar correctamente la instalación y configuración de un Worker Node en un clúster de Kubernetes.

## Duración aproximada
15 minutos

<br/>
## Instrucciones

1. **Acceso al Worker Node**
   - Ingresa al Worker Node usando SSH:
     ```bash
     ssh usuario@ip_worker_node
     ```
   - **Observación**: Asegúrate de que la dirección IP sea correcta y que tengas permisos de usuario con privilegios adecuados en el nodo, wnadmin y contraseña Netec_123.

<br/>

2. **Verificar Conexión con el Master Node**
   - Comprueba si el Worker Node está correctamente unido al clúster usando el siguiente comando en el Master Node:
     ```bash
     kubectl get nodes
     ```
   - **Observación**: Deberías ver el Worker Node listado como `Ready`. Si aparece como `NotReady`, es posible que haya problemas con la configuración de red o de `kubelet` en el nodo trabajador.

<br/>

3. **Verificar el Estado del Servicio Kubelet en el Worker Node**
   - Ejecuta el siguiente comando en el Worker Node para comprobar el estado del `kubelet`:
     ```bash
     sudo systemctl status kubelet
     ```
   - **Observación**: El servicio debe estar activo (`active (running)`). Si no lo está, intenta reiniciarlo usando:
     ```bash
     sudo systemctl restart kubelet
     ```
<br/>

4. **Verificar el Registro en el clúster**
   - Ejecuta este comando en el Worker Node para verificar que el nodo está registrado:
     ```bash
     sudo journalctl -u kubelet | grep "Node has joined"
     ```
   - **Observación**: Este mensaje confirma que el Worker Node ha establecido comunicación con el clúster. Si no aparece, revisa los logs de `kubelet` para identificar posibles errores.

<br/>
5. **Comprobar la Configuración de Red**
   - Verifica que las interfaces de red y el servicio `kube-proxy` funcionan correctamente:
     ```bash
     sudo systemctl status kube-proxy
     ```
   - **Observación**: La red es esencial para la comunicación entre los nodos. Si `kube-proxy` no está en ejecución, revisa la configuración del `cni` (Container Network Interface) y la conectividad de red del nodo.

<br/>
6. **Validar que el nodo puede ejecutar pods**
   - En el Master Node, despliega un pod de prueba en el Worker Node:
     ```bash
     kubectl run nginx-test --image=nginx --restart=Never --node-selector="kubernetes.io/hostname=worker-node-name"
     ```
   - **Observación**: Cambia `worker-node-name` por el nombre del Worker Node que aparece en `kubectl get nodes`. Luego, verifica el estado del pod con:
     ```bash
     kubectl get pod nginx-test
     ```
   - Si el pod no se ejecuta en el Worker Node, verifica la configuración de `kubelet` y los permisos del nodo.

<br/>
7. **Eliminar el Pod de Prueba**
   - Una vez verificada la correcta ejecución del pod, elimina el pod de prueba:
     ```bash
     kubectl delete pod nginx-test
     ```



## Resultado Esperado