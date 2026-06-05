pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'make build'
            }
        }
        stage('Test') {
            steps {
                sh 'make test'
            }
        }
        stage('Package') {
            steps {
                script {
                    app = docker.build("username/myapp:${env.BRANCH_NAME}")
                }
            }
        }
        stage('Publish') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        app.push()
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
