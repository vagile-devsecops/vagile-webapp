pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vagile-devsecops/vagile-webapp.git']])
            }
        }
        stage('maven build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8090/')], contextPath: 'webapp-vagile', war: '**/*.war'
            }
        }
    }
}
