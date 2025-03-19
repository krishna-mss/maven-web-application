pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git "https://github.com/krishna-mss/maven-web-application.git"
            }
        }
        stage('build maven'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonartoken') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}