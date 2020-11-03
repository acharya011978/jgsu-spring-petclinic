

pipeline {
    agent any

     
 stages {
        stage("Checkout") {
            echo "Job Name:  ${params.JOB_NAME}"
            steps { 
                    git branch: 'main', url: 'https://github.com/acharya011978/jgsu-spring-petclinic.git'
                 } 
         }
    
 stage ("Build") {
        steps{
                // Run Maven on a ec2 agent.
              sh 'mvn clean compile'
              
            }

      
        post {
                Always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                    }
                }
            
  }
        
 stage("Deploy"){
          echo "deploying the application"
          echo "deploying version: ${params.VERSION}"
   }
        
    }
 }
