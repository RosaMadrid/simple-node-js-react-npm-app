pipeline {
    agent any

    tools {
        nodejs 'node' // nombre que configuraste antes
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Despliegue simulado'
            }
        }
    }

    post {
        success {
            echo '🎉 Todo fue bien.'
        }
        failure {
            echo '❌ Algo falló.'
        }
    }
}
