# Práctica 1.2 Verificación de Ambiente de Curso

## Objetivo
Al finalizar esta actividad, serás capaz de verificar y asegurar que todos los componentes necesarios para el curso están instalados y configurados correctamente en el entorno de trabajo.

## Duración aproximada
25 minutos

## Instrucciones

1. **Consulta con tu instructor**

Pregunta a tu instructor cómo acceder al entorno de prácticas del curso y asegúrate de entender todas las instrucciones necesarias para su acceso este día y los días siguientes de clase.

2. **Configura Git**

Asegúrate de tener configurados tu nombre y correo en Git. Esto se puede hacer con los siguientes comandos:

```bash
 
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
git config --list

````

3. **Clona el repositorio del curso**

Clona el repositorio proporcionado por el instructor para acceder a los archivos de práctica. Puedes hacerlo con:

```bash
 
git clone <URL_del_repositorio>

```

4. **Verifica Maven (Opcional)**

Confirma que tienes Maven instalado y configurado en tu sistema. Esto es útil en caso de que necesites construir proyectos fuera del entorno de Spring Boot. Verifica la instalación ejecutando:

```bash

mvn -v

```

**Nota:** Aunque no es indispensable tener Maven configurado fuera del entorno de Spring, puede ser útil para tareas específicas.


5. **Verifica Gradle (Opcional)**

Asegúrate de que Gradle esté instalado y configurado. Para verificar la instalación, utiliza:

```bash
gradle -v
```

6. **Verifica Java 21**

Comprueba que tienes instalada la versión 21 de Java. Puedes verificar la versión ejecutando:

```bash
javac --version
java --version
```

7. **Verifica Visual Studio Code (VSC)**

Asegúrate de tener Visual Studio Code instalado, ya sea pulsando el ícono en la aplicación en el escritorio o iniciando en la línea de comandos lo siguiente:

```bash
# Recuerda que el . significa el actual directorio de trabajo
code .
```

8. ** Instala los plugins requeridos en VSC **

Verifica que tienes los siguientes plugins instalados en Visual Studio Code para facilitar el desarrollo:

- Extension Pack for Java v0.29.0
- Docker v1.29.3
- Kubernetes YAML Formatter v1.1.0
- Kubernetes v1.3.18


## Resultado Esperado
