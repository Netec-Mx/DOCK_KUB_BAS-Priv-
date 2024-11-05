# Práctica 2.3 Agregación de un nuevo Worker Node al Clúster.

## Objetivo

Al finalizar esta actividad, serás capaz de verificar correctamente la instalación y configuración de un Worker Node en un clúster de Kubernetes.


## Duración aproximada

30 minutos

## Instrucciones

<br/>

**Paso 1: Intalar paquetería básica**

    - Actualiza los repositorios e instala los paquetes necesarios para el transporte de paquetes HTTPS.

    ```bash
sudo apt-get update 
sudo apt install apt-transport-https curl -y
    ```

<br/>

**Paso 2: Preconfigurar el Networking**

    - Configura los módulos necesarios para Kubernetes y aplica los parámetros de red.

    ```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

    ```

    - Define los parámetros de `sysctl` necesarios para el funcionamiento de Kubernetes

    ```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

# Aplicar parámetros de sysctl
sudo sysctl --system

    ```

    - Verifica que los módulos estén correctamente cargados

    ```bash
lsmod | grep br_netfilter
lsmod | grep overlay

    ```

    - Confirma que los parámetros de red estén configurados.

    ```bash
sysctl net.bridge.bridge-nf-call-iptables net.bridge.bridge-nf-call-ip6tables net.ipv4.ip_forward

    ```

<br/>

**Paso 3: Deshabilitar el Swap**

```bash

```

<br/>

**Paso 4: Intalar containerd**



<br/>

**Paso 5: Habilitar containerd como Runtime de Contenedor**

<br/>

**Paso 6: Reiniciar containerd**


<br/>

**Paso 7: Actualizar e instalar paquetería necesaria**


<br/>

**Paso 8: Descargar y agregar repositorios de Kubernetes**

<br/>

**Paso 9: Instalar kubelet, kubeadm y kubectl**


<br/>

**Paso 10: Unir el Worker Node al Control Plane**


## Resultado Esperado