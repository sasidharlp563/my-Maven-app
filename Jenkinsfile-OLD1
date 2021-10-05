pipeline{
    agent any 
    stages{
        stage("SCM checkout"){
            steps{
              git credentialsId: 'github', url: 'https://github.com/jagadeesh-nani/my-app.git'  
            }
        }
        stage("MAVEN build"){
            steps{
              sh 'mvn clean package  #-DskipTests=true#'
            }
        }
    }
}
