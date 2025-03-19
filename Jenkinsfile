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
    }
}