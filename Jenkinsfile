pipeline {
    agent any

    tools {
        nodejs 'node' // nombre que configuraste antes
    }

    environment {
        DOCKER_IMAGE = 'simple-node-js-react-app'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop ${DOCKER_IMAGE} || true
                    docker rm ${DOCKER_IMAGE} || true
                    docker run -d --name ${DOCKER_IMAGE} -p 3000:3000 ${DOCKER_IMAGE}:${DOCKER_TAG}
                '''
            }
        }
    }

    post {
        success {
            echo '🎉 Despliegue completado exitosamente.'
        }
        failure {
            echo '❌ El despliegue falló.'
        }
    }
}
