pipeline {
   
    agent any
    // Se declaran las herramientas que se utilizarán, en este caso Maven.
    tools {
        maven 'Maven_3_8_7'
    }

    // El pipeline se divide en etapas para organizar los pasos.
    stages {
         
        // Se compila el código y se ejecuta un escaneo de seguridad con SonarQube (SAST) .
        stage('CompileandRunSonarAnalysis') {
            steps {
                // Se usa el token de SonarQube de forma segura para autenticarse.
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    // El comando de Maven inicia el análisis estático en el código fuente.
                    bat '''
                    mvn -Dmaven.test.failure.ignore verify sonar:sonar ^
                    -Dsonar.login=%SONAR_TOKEN% ^
                    -Dsonar.projectKey=easybuggy ^
                    -Dsonar.host.url=http://localhost:9000/
                    '''
                }
            }
        }
        
        
        // Se construye una imagen de Docker a partir del código.
        stage('Build') {
            steps {
                // Se utilizan las credenciales para acceder al registro de Docker.
                withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                    script {
                        // Se crea la imagen de Docker para la aplicación.
                        app = docker.build("asecurityguru/testeb")
                    }
                }
            }
        }
        
        
        // Se escanea la imagen de Docker para detectar vulnerabilidades.
        stage('RunContainerScan') {
            steps {
                // Se usa el token de Snyk para autenticar el escaneo.
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    script {
                        // Se ejecuta la herramienta Snyk para probar la seguridad del contenedor.
                        try {
                            bat("C:\\snyk-win.exe  container test asecurityguru/testeb")
                        } catch (err) {
                            echo err.getMessage()
                        }
                    }
                }
            }
        }
        
       
        // Se escanean las dependencias del proyecto para encontrar vulnerabilidades conocidas (SCA).
        stage('RunSnykSCA') {
            steps {
                // Se utiliza el token de Snyk.
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    // El comando de Maven ejecuta el escaneo de dependencias con Snyk.
                    bat("mvn snyk:test -fn")
                }
            }
        }
        
        
        // Se escanea la aplicación en ejecución para encontrar vulnerabilidades (DAST).
        stage('RunDASTUsingZAP') {
            steps {
                // Se ejecuta la herramienta OWASP ZAP para realizar un escaneo dinámico.
                bat("C:\\ZAP_2.16.0_Crossplatform\\ZAP_2.16.0\\zap.sh -port 9393 -cmd -quickurl https://www.example.com -quickprogress -quickout C:\\ZAP_2.16.0_Crossplatform\\ZAP_2.16.0\\Output.html")
            }
        }

        
        // Se escanean los archivos de configuración de infraestructura para detectar malas configuraciones de seguridad (IaC).
        stage('Checkov Scan') {
            steps {
                // Se utiliza la herramienta Checkov para analizar la seguridad del código de infraestructura.
                bat '''
                echo Ejecutando Checkov con python -m ...
                C:\\Users\\ASUS\\AppData\\Local\\Programs\\Python\\Python312\\python.exe -m checkov.main -s -f main.tf --output cli 2>&1
                '''
            }
        }
    }
}
