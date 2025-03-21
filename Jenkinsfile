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
        } /*
        stage('static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-key') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        } */
        stage('nexus'){
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'maven-web-application',
                             classifier: '',
                              file: 'target/maven-web-application.war',
                               type: ''
                               ]
                               ], 
                               credentialsId: 'nexus-key',
                                groupId: 'com.mt',
                                 nexusUrl: '65.0.204.102:8081', 
                                 nexusVersion: 'nexus3',
                                  protocol: 'http', 
                                  repository: 'maven-releases', 
                                  version: '1.0.1'
                }
            }
        }
    }
}