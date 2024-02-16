pipeline{
    agent any
    stages{
        stage("SCM code clone"){
            steps{
                git credentialsId: 'GITHUB',
                url: 'https://github.com/sasidharlp563/my-Maven-app.git'
            }
        }
        stage("Maven build"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Nexus Artifact"){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'myweb', 
                classifier: '', 
                file: 'target/myweb-0.0.16.war', type: 'war']], 
                credentialsId: 'Nexus3', 
                groupId: 'in.javahome', 
                nexusUrl: '172.31.1.97:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'my-first-job-release', 
                version: '0.0.16'
            }
        }
    }
}
