pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('git checkout'){
            steps{
                git branch:'master', url:'https://github.com/krishna-mss/maven-web-application.git'
            }
        }
    }
}