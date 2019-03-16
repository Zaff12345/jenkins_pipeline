pipeline {
    agent any

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
                withMaven(maven : 'Localmaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'Localmaven') {
                    sh 'mvn install'
                }
            }
        }
    }
}
