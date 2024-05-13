pipeline {
    agent any
    stages {
        stage('Package') {
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
                bat 'docker tag teedy-test nomathexpectation/teedy-test:k8s'
                bat 'docker push nomathexpectation/teedy-test:k8s'
            }
        }
        stage('k8s') {
            steps {
                bat 'kubectl set image deployments/hello-node teedy-test=nomathexpectation/teedy-test:k8s'
            }
        }
    }
}
