pipeline {
    agent any

    tools {
        nodejs "Node25" // Usamos solo Node.js, eliminamos dockerTool para evitar el error
    }

    stages {
        stage('Instalar Dependencias') {
            steps {
                sh 'npm install'
            }
        }

        stage('Ejecutar Aplicacion') {
            steps {
                // Esta variable evita que Jenkins mate la aplicación cuando termine el pipeline
                withEnv(['JENKINS_NODE_COOKIE=dontKillMe']) {
                    // Detenemos cualquier versión anterior de la app que esté corriendo
                    sh 'pkill node || true'
                    // Ejecutamos la app en segundo plano
                    sh 'nohup node index.js > app.log 2>&1 &'
                }
            }
        }
    }
}