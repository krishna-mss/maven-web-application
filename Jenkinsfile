pipeline{
    agent any
    stages{
        stage('Git Checkout'){
            steps{
                git branch:"master", url:"https://github.com/krishna-mss/maven-web-application.git"
            }
        }
        stage('Build Maven'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-key') {
                     sh 'mvn clean package sonar:sonar'
                 }
                }
            }
        }
    }
}