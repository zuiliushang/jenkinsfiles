pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2 -p 8099:8099' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
	stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
	stage('Deliver') { 
            steps {
                sh 'whoami'
                sh '/bin/bash ./jenkins/scripts/deliver.sh' 
                sh 'java -jar target/spordniar-app-0.0.1-SNAPSHOT.jar'
            }
        }
    }
}
