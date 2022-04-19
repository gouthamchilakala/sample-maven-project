pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{

                  nexusArtifactUploader artifacts: [
                    [
                      artifactId: 'offers', classifier: '', 
                      file: 'target/offers-1.1-release.jar', type: 'jar'
                    ]
                  ], 
                    credentialsId: '', 
                    groupId: 'flipkart', 
                    nexusUrl: '172.31.44.213:8081', 
                    nexusVersion: 'nexus2', 
                    protocol: 'http', repository: 'http://18.222.140.4:8081/repository/sampleapp-release/', 
                    version: '1.1-release'
                    }
            }
        }
    }
}
