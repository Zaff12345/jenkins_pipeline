pipeline {
    agent { label 'mavenlabel' }

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'MyMaven') {
                    sh 'mvn clean compile'
                }
            }
        }
        
            
        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'MyMaven') {
                    sh 'mvn test'
                }
            }
        }
        
                
        stage ('Build on Slave Stage') {

            steps {
                withMaven(maven : 'MyMaven') {
                    sh 'mvn package'
                }
            }
        }
        
        
        stage ('Deploy to Tomcat') {
       
            steps {
                sshagent (credentials: ['tomcat']) {
                    sh 'ssh -o StrictHostKeyChecking=no target/*.jar ec2-use@35.166.214.243:/opt/tomcat/webapps/'
                }
            }
        }
        
        stage ('Building and Integrating Sonar') {

            steps {
                withSonarQubeEnv('Sonarqube') {
                    sh 'mvn package sonar:sonar'
                }
            }
        }
        
        
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'MyMaven') {
                    sh 'mvn install'
                }
            }
        }
    }
}
