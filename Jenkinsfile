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
                    sh 'scp -o StrictHostKeyChecking=no /home/ec2-user/jenkins-slave/workspace/agent-job/target/*.jar ec2-user@52.26.75.65:/opt/tomcat/webapps/'
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
