pipeline {
    agent {
        docker {
            image 'maven:3-jdk-11'
            args '-v /root/.m2:/root/.m2'
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
                sh 'pwd'
                sh 'ls -l ./scripts/'
                sh 'chmod +x ./scripts/deliver.sh'
                sh './scripts/deliver.sh'
            }
        }
    }
}
