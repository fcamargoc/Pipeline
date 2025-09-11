# Laboratorio DevSecOps 

Crear un proceso de entrega de software seguro y automatizado que identifique y mitigue vulnerabilidades en múltiples frentes código, dependencias, contenedores e infraestructura para garantizar la calidad y la robustez en seguridad de la aplicación antes de su despliegue.


## Prerequisitos
### 1. instalar Jenkins
### 2. instalar Docker
### 3. instalar Maven
### 4. instalar SnykCLI - crear cuenta en la web
### 5. java
### 6. Owasp Zap
### 7. Python
### 8. Checkov

Configurar Python como variable de entorno en tu pc. 

## Configuración del entorno 

### 1. Desplegar el contenedor de sonarqube usando docker

docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

### 2. Agregar en Jenkins la herramienta de Maven para que pueda ejecutarlo. 

<img width="1382" height="947" alt="image" src="https://github.com/user-attachments/assets/4d6557c9-144f-47fa-a0d7-a9d73e680625" />

### 3. Instalar docker plugin en Jenkins

<img width="1736" height="635" alt="image" src="https://github.com/user-attachments/assets/972fdd33-a316-44b2-bfd1-b43b23f60db9" />


## 4. Crear el proyecto y token de autenticacion en sonarqube

### 4.1 Crea un proyecto local 

<img width="1175" height="782" alt="image" src="https://github.com/user-attachments/assets/d486ca2d-f9cd-4848-a212-8a6d6878d704" />

### 4.2 Para la creación del token se deben dirigir a configuración de cuenta > seguridad. alli crea el token y selecciona el proyecto

<img width="1888" height="937" alt="image" src="https://github.com/user-attachments/assets/107c37aa-8afa-40e2-9b26-967fd47d489b" />

### 5. Creación del token de Snyk

<img width="1897" height="857" alt="image" src="https://github.com/user-attachments/assets/d7ea8347-ba6c-4e52-b769-dfd97bcb9a0a" />

### 6. Creación de los tokens en Jenkins

<img width="1892" height="701" alt="image" src="https://github.com/user-attachments/assets/51dead35-0554-466d-b95c-38f29bc4774d" />

Para el token de Dockerlogin utilizas las credenciales de Docker hub 

## 7. Creación de Pipeline en Jenkins

Al momento de crear el Pipeline se debe configurar los siguientes parametros 

### 7.1 Ingresar la URL donde se encuentra el proyecto 
<img width="1877" height="893" alt="image" src="https://github.com/user-attachments/assets/bf415827-3694-4c82-9f48-acaebb23056d" />

### 7.2 Especificar la rama y el nombre del archivo que define la ejecución del Pipeline

<img width="1852" height="893" alt="image" src="https://github.com/user-attachments/assets/b862e666-1283-41a8-8ed1-681add62f303" />

Ya realizado todos los pasos anteriores puedes ejecutar el Build en Jenkins y observar el resultados de cada uno de los scaners.

# Jenkins
<img width="1887" height="737" alt="image" src="https://github.com/user-attachments/assets/ddaec446-f3dd-46cf-b57f-13c6f431ce80" />

# Sonarqube

<img width="1592" height="951" alt="image" src="https://github.com/user-attachments/assets/32789d58-568e-4c64-bc9e-90e120890fa2" />

# Synk container test

<img width="1872" height="957" alt="image" src="https://github.com/user-attachments/assets/99bc83b3-8c3f-4b83-adc7-55b742f72e6b" />

# Synk SCA

<img width="1824" height="900" alt="image" src="https://github.com/user-attachments/assets/579f222f-7159-4be7-a5ba-8d74e9e98536" />

# Owasp Zap DAST 

<img width="1561" height="969" alt="image" src="https://github.com/user-attachments/assets/1b9fcf39-2be8-450a-9f3f-b79a2a5fd0ba" />

# Checkov IaC

<img width="1860" height="887" alt="image" src="https://github.com/user-attachments/assets/0831a017-40e5-4df1-b749-92dbed00d358" />



