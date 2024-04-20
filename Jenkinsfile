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
