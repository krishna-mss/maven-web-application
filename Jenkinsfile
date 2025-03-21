pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git 'https://github.com/krishna-mss/maven-web-application.git'
            }
        }
        stage('mvn build'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
}