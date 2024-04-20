pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clonar el repositorio
                    git branch: 'master', url: 'https://github.com/8infinitecloud/juice-shop'
                }
            }
        }

        stage('Build Node.js Application') {
            steps {
                script {
                    // Ejecutar el comando de construcción de Node.js
                    sh 'npm install'
                    sh 'npm run build'  // Suponiendo que este comando construye la aplicación
                }
            }
        }
        
        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                script {
                    // Define los argumentos adicionales para Dependency-Check
                    def dependencyCheckArgs = '''
                        -o './'
                        -s './'
                        -f 'ALL' 
                        --prettyPrint
                    '''

                    // Ejecuta Dependency-Check
                    dependencyCheck additionalArguments: dependencyCheckArgs, odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                    
                    // Publica el reporte generado por Dependency-Check
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
            }
        }
    }
}
