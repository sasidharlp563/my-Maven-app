pipeline{
    agent any
    stages{
        stage("SCM Checkout"){
            steps{
                git credentialsId: 'github',
                url: 'https://github.com/jagadeesh-nani/my-app.git'
            }
        }
        
        stage("Maven Build"){
            steps{
                sh 'mvn clean package'
            }
        }
        
        stage("Nexus"){
            steps{
                nexusArtifactUploader artifacts: 
                [
                    [artifactId: 'myweb', classifier: '', file: 'target/myweb-0.0.16.war', type: 'war']
                ], 
                    credentialsId: 'nexus3', 
                    groupId: 'in.javahome', 
                    nexusUrl: '54.177.100.42:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'naniapp-release', 
                    version: '0.0.16'   
                
            }
        }
        stage("Tomcat-dev"){
            steps{
              sshagent(['tomcat-dev']) {
                  sh 'scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@172.31.1.202:/opt/tomcat8/webapps'
                  sh "ssh ec2-user@172.31.1.202 /opt/tomcat8/bin/shutdown.sh"
                  sh "ssh ec2-user@172.31.1.202 /opt/tomcat8/bin/startup.sh"
                    }  
            }
        }
    }
}
