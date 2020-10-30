

pipeline {
    agent any

    parameters{
        CODE_CHANGES = getGitChanges()
        JOB_NAME = "petAnimals_pipeline"
        string(name: 'VERSION', defaultValue: '1.0', description: 'string: Version to deploy on production server')
        choice(name: 'VERSION', choices: ['1.0','1.1','1.2'], descriptoin: 'choice: Version to deploy on production server')
        booleanParam(name: 'EXECUTE_TEST', defaultValue: true, description: 'boolean: Version to deploy on production server')
            }
  
    stages {
        stage('Checkout') {
            echo "Job Name:  ${params.JOB_NAME}"
            steps { 
                    git branch: 'main', url: 'https://github.com/acharya011978/jgsu-spring-petclinic.git'
                 } 
             }
    
        stage ('Build') {
        steps{
                // Run Maven on a ec2 agent.
              sh 'mvn clean compile'
            }

         }

        when{
            expression{
                params.EXECUTE_TEST
                    }
              }
      
        post {
                Always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                    }
                }
        
        
      stage("Deploy"){
          echo "deploying the application"
          echo "deploying version: ${params.VERSION}"
        }
    }
 }
