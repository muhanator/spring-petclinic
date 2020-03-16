//Building a declarative pipeline
pipeline {
    agent any
    //main three stages
    stages {
        stage('Build') {
            steps {
                bat './mvnw clean' 
            }
        }
        stage('Test') {
            steps {
                bat './mvnw test' 
            }
        }
        stage('Package') {
            steps {
                bat './mvnw package' 
            }
        }
        //only run this stage if we are in the master branch
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                bat './mvnw deploy' 
            }
        }
    }
    post {
        success {
            mail to: 'muhanator1997@gmail.com',
                subject: "Successful Build! ${currentBuild.fullDisplayName}",
                body: " ${env.BUILD_URL}"
        }
        failure {
            mail to: 'muhanator1997@gmail.com',
                subject: "Fail Build! ${currentBuild.fullDisplayName}",
                body: " ${env.BUILD_URL}"
        }
    }
}