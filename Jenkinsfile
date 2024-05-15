pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'examen:latest'

    }

    stages {
        stage('Source code management') {
            steps {
                git "https://github.com/eyanaffeti/expensse-tracker.git"
            }
        }
        stage('Installation des dpendances') {
            steps {
                sh 'npm install'  
            }
        }
        stage('automation server') {
            steps {

                script {
                    sh 'sonar-scanner'
                }
            }
        }
        stage('Container Service') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Production') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl rollout status deployment/examen'
                }
            }
        }
    }

}
