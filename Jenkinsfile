pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Dewdrop-bee/dawn-app.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t dawn:${env.BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Push Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push dawn:${env.BUILD_NUMBER}'
                }
            }
        }
    }
}
