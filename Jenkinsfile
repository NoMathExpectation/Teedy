pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -DskipTests clean package'
            }
        }
        stage('Doc') {
                steps {
                    bat 'mvn site --fail-never'
                }
            }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
        }
    }
}
