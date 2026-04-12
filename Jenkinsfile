pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
                }
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                mkdir -p $WORKSPACE/deployed/
                cp target/*.war $WORKSPACE/deployed/
                echo "Deployed WAR to $WORKSPACE/deployed/"
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Run integration tests here"'
            }
        }
    }
}
