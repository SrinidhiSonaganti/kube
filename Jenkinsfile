pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SrinidhiSonaganti/kube.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t mykube:latest .'
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    sh 'echo Srinidhiraviprasad@04 | docker login -u srinidhisonaganti --password-stdin'
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    sh 'docker tag mykube:latest srinidhisonaganti/my-kube:latest'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push srinidhisonaganti/my-kube:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f node-app-deployment.yaml'
                    sh 'kubectl apply -f node-app-service.yaml'
                }
            }
        }
    }
}
