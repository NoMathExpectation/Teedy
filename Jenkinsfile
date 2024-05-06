pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -DskipTests clean package'
            }
        }
        stage('Build') {
            steps {
                bat 'docker build -t teedy-test .'
            }
        }
        stage('Publish') {
            steps {
                bat 'docker push teedy-test'
            }
        }
        stage('Create') {
            steps {
                bat 'docker run --rm -d -p 8082:8080 teedy-test'
                bat 'docker run --rm -d -p 8083:8080 teedy-test'
                bat 'docker run --rm -d -p 8084:8080 teedy-test'
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
