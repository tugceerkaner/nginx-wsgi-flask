pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
        DOCKER_HUB_USERNAME = 'tugceerkaner'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/techpodium/nginx-wsgi-flask'
                git 'https://github.com/tugceerkaner/nginx-wsgi-flask.git'
            }
        }
        stage('Build Flask Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_USERNAME}/flask-app:latest", './flask')
                }
            }
        }
        stage('Build Nginx Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_USERNAME}/nginx-proxy:latest", './nginx')
                }
            }
        }
        stage('Push Flask Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("${DOCKER_HUB_USERNAME}/flask-app:latest").push()
                    }
                }
            }
        }
        stage('Push Nginx Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("${DOCKER_HUB_USERNAME}/nginx-proxy:latest").push()
                    }
                }
            }
        }
        stage('Deploy Application') {
            steps {
                script {
                    sh 'docker-compose -f compose.yaml down'
                    sh 'docker-compose -f compose.yaml up -d'
                }
            }
        }
    }
    /*post {
        always {
            script {
                sh 'docker-compose -f compose.yaml down'
            }
        }
    }*/
}