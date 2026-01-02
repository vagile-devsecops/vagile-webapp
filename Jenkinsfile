pipeline {
    agent any

    stages {
        stage('cleanup') {
            steps {
                deleteDir()
            }
        }
        stage('git'){
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajukalyanit/kalyanit.git']])
            }
        }
        stage('maven'){
            steps {
               bat 'mvn clean package'
            }
        }
         stage('tomcat'){
            steps {
               bat 'mvn tomcat7:deploy'
            }
        }
    }
      post {
        always {
            // This step will always be executed
            emailext (
                to: 'nagapatukuru@gmail.com',
                subject: "Build ${currentBuild.result}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${currentBuild.result}: ${env.JOB_NAME} #${env.BUILD_NUMBER} \n\n${currentBuild.currentResult}\n\nCheck console output at ${env.BUILD_URL}",
                attachLog: true,
                replyTo: 'noreply@example.com'
            )
        }
    }
}
