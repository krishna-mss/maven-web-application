
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
        }
        stage('upload artifact'){
            steps{
                script{

                    def readPomVersion = readMavenPom file: "pom.xml"

                    def nexusRepo = readPomVersion.version.endswith('SNAPSHOT') ? "maven-snapshots":"maven-releases"

                     nexusArtifactUploader artifacts: 
                  [
                    [
                        artifactId: 'maven-web-application',
                         classifier: '', 
                         file: 'target/maven-web-application.war',
                          type: 'war'
                          ]
                          ],
                           credentialsId: 'nexus-auth',
                            groupId: 'com.mt',
                             nexusUrl: '3.110.186.253:8081',
                              nexusVersion: 'nexus3',
                               protocol: 'http',
                                repository: 'nexusRepo',
                                 version: '${readPomVersion.version}'
                }
            }
        }
   }
}