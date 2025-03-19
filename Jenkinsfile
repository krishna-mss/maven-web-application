pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git credentialsId: 'gittoken', url: 'https://github.com/krishna-mss/maven-web-application.git'
            }
        }
    }
}