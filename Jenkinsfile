pipeline {
    agent any
    tools {
        jdk 'JDK 17'
        maven 'Maven 3.8.6'
    }
    stages {
        stage('Install Tools') {
            steps {
                bat 'choco install openjdk17 maven -y'
            }
        }
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