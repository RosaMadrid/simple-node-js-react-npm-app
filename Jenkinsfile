pipeline {
    agent any

    tools {
        nodejs "NodeJS_18"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/RosaMadrid/simple-node-js-react-npm-app.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
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
                sh 'docker build -t react-demo-app .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker run -d -p 3000:3000 react-demo-app'
            }
        }
    }

    post {
        failure {
            echo "❌ Algo falló en el pipeline"
        }
        success {
            echo "✅ Despliegue completo"
        }
    }
}
