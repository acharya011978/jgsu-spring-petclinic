

pipeline {
    agent any
    
tools{ 
    maven 'maven'
}

     
 stages {
        stage("Checkout") {
           
            steps { 
                    echo 'Job Name:  ${params.JOB_NAME}'
                    git branch: 'main', url: 'https://github.com/acharya011978/jgsu-spring-petclinic.git'
                 } 
         }
    
 stage ("Build") {
        steps{
                // Run Maven on a ec2 agent.
              sh 'mvn clean install'
              
            }

      
        post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                    }
                }
            
        }
        
 stage("Deploy"){
        steps {
            echo 'deploying the application'
           // echo 'deploying version: ${params.VERSION}'
            }
        }
        
    }
 }
