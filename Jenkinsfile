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
                script{
                    sh 'mvn clean install'
                }
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
        /*
        stage('quality status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-key'
                }
            }
        } 
        stage('upload artifacte'){
            steps{
                script{

                    def readPomVersion = readMavenPom file: 'pom.xml'
                    def nexusRepo = readPomVersion.version.endswith('SNAPSHOT') ? "maven-snapshot":"maven-release"
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
                    nexusUrl: '13.201.63.201:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'maven-release', 
                    version: '2.0.0'
                }
            }
        } */
        stage('docer image'){
            steps{
                script{
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID krishna122/$JOB_NAME:v1.$BUILD_ID'
                }
            }
        }
    }
}