
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
                   withSonarQubeEnv(credentialsId: 'sonar-key') {
                    sh 'mvn clean package sonar:sonar'
                   }
                }
            }
        }

        stage('quality status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-key'
                }
            }
        }  /*
        stage('upload artifact'){
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'maven-web-application',
                             classifier: '',
                              file: 'target/maven-web-application.war', 
                              type: 'war'
                              ]
                              ],
                               credentialsId: 'nexus-api',
                                groupId: 'com.mt',
                                 nexusUrl: '13.233.161.39:8081', 
                                 nexusVersion: 'nexus3', 
                                 protocol: 'http',
                                  repository: 'maven-releases', 
                                  version: '1.0.1'
                }
            }
        } 
        stage('creage docker image'){
            steps{
                script{
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID krishna122/$JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID krishna122/$JOB_NAME:latest'
                }
            }
        }*/
   }
}