pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
                git(branch 'main', url:'https://github.com/vagile-devsecops/vagile-webapp.git' )
            }
        }
        stage('maven build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8090/')], contextPath: 'webapp-vagile', war: '**/*.war'
            }
        }
    }
