pipeline {
    agent any
    tools {
        maven 'Maven 3.8.6' // Укажите название Maven из настроек Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
               checkout([
                                   $class: 'GitSCM',
                                   branches: [[name: '*/main']],
                                   extensions: [],
                                   userRemoteConfigs: [[
                                       credentialsId: 'test123123123',
                                       url: 'https://github.com/tokyoinfire/P_P_3.1.1.git'
                                   ]]
                               ])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package' // Собирает JAR
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("your-dockerhub/test-app:${env.BUILD_ID}")
                }
            }
        }
        stage('Deploy to k8s') {
            steps {
                sh 'kubectl apply -f k8s-manifests/' // Применяет манифесты
            }
        }
    }
}