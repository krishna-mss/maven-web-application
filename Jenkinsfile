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
       stage('Build Maven'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Static Code Analysis'){
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
