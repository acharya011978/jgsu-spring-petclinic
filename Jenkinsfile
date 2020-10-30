#! /usr/bin/env groovy

pipeline {
    agent any

    parameters{
        string(name: 'VERSION', defaultValue: '1.0', description: 'string: Version to deploy on production server')
        choice(name: 'VERSION', choices: ['1.0','1.1','1.2'], descriptoin: 'choice: Version to deploy on production server')
        booleanParam(name: 'EXECUTE_TEST', defaultValue: true, description: 'boolean: Version to deploy on production server')
            }
    stages {
        stage('Checkout') {
            steps { 
                // Get code from a GitHub repository
                 git branch: 'main', url: 'https://github.com/acharya011978/jgsu-spring-petclinic.git'
                } 
             }
    stage ('Build') {
        steps{
                // Run Maven on a ec2 agent.
                sh './mvnw clean compile'
            }

         }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                Always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                    }
                }
    }
 }
