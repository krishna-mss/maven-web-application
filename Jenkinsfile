pipeline{
    agent any
    tools {
        maven 'Maven 3.9.8'  // Name you configured in Global Tool Configuration
    }
    stages{
        stage('git checkout'){
            steps{
                git 'https://github.com/krishna-mss/maven-web-application.git'
            }
        }
        stage('Build Maven'){
            steps{
                sh "mvn clean installs"
            }
        }   
    }
}