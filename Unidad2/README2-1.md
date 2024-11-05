# Práctica 2.1 Verificación de Instalación del Master Node  

## Objetivo 
Al finalizar esta actividad, serás capaz de verificar correctamente la instalación y configuración del nodo maestro (Master Node) en un clúster de Kubernetes

## Duración aproximada
15 minutos


**Requisitos previos:**  
- La instalación de Kubernetes ya está completada en un sistema Ubuntu Server 20.04.

---

## Instrucciones:

1. **Acceso al nodo maestro**  
   - Inicia sesión en el nodo maestro utilizando SSH:
     ```bash
     ssh usuario@direccion-ip-del-master-node
     ```
    - **Nota:** La contraseña de las máquinas podría ser Netec_123, esta pudiera cambiar, tu instructor la confirmará.

2. **Verificar el estado del clúster**  
   - Ejecuta el siguiente comando para verificar si el clúster de Kubernetes está activo y en funcionamiento:
     ```bash
     kubectl get nodes
     ```
   - Asegúrate de ver el nodo maestro en la lista con el estado "Ready".

3. **Comprobar el estado de los componentes del nodo maestro**  
   - Para confirmar que todos los componentes del nodo maestro están operativos, ejecuta:
     ```bash
     kubectl get pods -n kube-system
     ```
   - Verifica que todos los pods del sistema están en estado "Running" o "Completed".

4. **Comprobar la versión de Kubernetes**  
   - Confirma la versión de Kubernetes instalada en el nodo maestro:
     ```bash
     kubectl version --short
     ```
   - Anota la versión para validar que es la esperada para tu entorno.

5. **Verificar configuración de red**  
   - Ejecuta el siguiente comando para verificar la configuración de red del nodo maestro:
     ```bash
     kubectl cluster-info
     ```
   - Asegúrate de que los componentes de control del clúster (kube-apiserver, etcd, kube-scheduler, kube-controller-manager) tienen sus URL configuradas correctamente.

6. **Validar la instalación del kubeconfig**  
   - Verifica que el archivo de configuración `kubeconfig` esté en la ubicación predeterminada y contenga la configuración correcta para el nodo maestro:
     ```bash
     cat ~/.kube/config
     ```
   - Asegúrate de que la configuración esté correcta para acceder al clúster desde el nodo maestro.

7. **Verificación del SWAP**
    - Ejecuta el siguiente comando para verificar el estado del swap
      ```bash
     sudo swapon --show
     free -h
     ```
    - Si el primer comando no muesta ninguna salida, el swap está deshabilitado.
    - El la salida del segundo comando, el valodr de la columna "Swap" debería ser cero si el swap está desactivado.

    - Para asegurarte de que el swap se deshabilite permanentemente después de cada reinicio, verifica el contenido del archivo `/etc/fstab`, la(s) linea(s) con swap deberán de estar comentadas.



8. **Finalizar**  
   - Tras verificar todos los puntos anteriores, confirma que el nodo maestro está correctamente configurado y listo para operar en el clúster de Kubernetes.



## Resultado Esperado


