# Práctica 2.5 Ejercicios Básicos K8s

## Objetivo
Al finalizar esta actividad, serás capaz de aplicar comandos y configuraciones básicas en Kubernetes para gestionar y monitorear recursos como Pods, Namespaces y Deployments.


## Duración aproximada
30 minutos

## YAMLs

- podsP3.yaml

```yaml
```

## Instrucciones

- Realiza los siguientes ejercicios:

# Cuestionario de Kubernetes - Unidad 2

1. **Lista la cantidad de Pods que se encuentran dentro del namespace `kube-system`.**

2. **Lista todos los Pods que se encuentren dentro del clúster.**

3. **Crea un Pod de manera imperativa que use la imagen `ubuntu:20`.**

4. **Usando la CLI de Kubernetes, genera el YAML que te permita crear un Pod que use la imagen `alpine`.**

5. **Usando YAML, crea un Pod que use la imagen `node:18.17-slim`.**

6. **Crea un namespace con el formato `<nombre_compañía_abreviado>-dev`.**

7. **Despliega un ReplicaSet de nombre `dev-ntc` en el nuevo namespace que use la imagen `alpine` y tenga 3 réplicas.**

8. **Elimina un Pod del ReplicaSet `dev-ntc` y explica qué sucede.**

9. **Crea un Deployment de nombre `backend` de 4 réplicas que use la imagen `python:3.11` y que exponga el puerto `8888`.**

10. **Realiza los cambios necesarios para que todos los Pods del Deployment `backend` estén en estado "Running".**


## Resultado Esperado