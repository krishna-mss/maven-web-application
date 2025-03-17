pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git "url:https://github.com/krishna-mss/maven-web-application.git"
            }
        }
        stage('Build Maven'){
            steps{
                sh 'mvn clean install'
            }
        }   
    }
}