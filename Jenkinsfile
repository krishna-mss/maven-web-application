pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
               git 'https://github.com/krishna-mss/maven-web-application.git'
            }
        }
        stage('build maven'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
}