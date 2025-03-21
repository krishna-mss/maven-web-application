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
        stage('static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-key') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage('quality statu'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-key'
                }
            }
        }
        stage('nexus'){
            steps{
                script{

                    def pom = readMavenPom file: 'pom.xml'

                    def nexusRepo = pom.version.endswith("SNAPSHOT") ? "maven-snapshots" : "maven-releases"

                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'maven-web-application',
                             classifier: '',
                              file: 'target/maven-web-application.war',
                               type: 'war'
                               ]
                    ], 
                    credentialsId: 'nexus-key',
                    groupId: 'com.mt',
                     nexusUrl: '3.108.223.39:8081',
                     nexusVersion: 'nexus3',
                     protocol: 'http',
                    repository: 'nexusRepo',
                    version: "${pom.version}"
                            
                }
            }
        }
        
    }
}