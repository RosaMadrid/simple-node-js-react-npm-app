pipeline {
    agent any

    tools {
        nodejs 'node' // Asegúrate de tener esta herramienta configurada en Jenkins
    }

    environment {
        IMAGE_NAME = 'simple-node-js-react-app'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/RosaMadrid/simple-node-js-react-npm-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker --version' // Verifica si docker está accesible
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 3000:80 --name react-app $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post {
        failure {
            echo '❌ El despliegue falló.'
        }
        success {
            echo '✅ Despliegue realizado con éxito.'
        }
    }
}

