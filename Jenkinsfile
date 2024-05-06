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
                bat 'docker tag teedy-test nomathexpectation/teedy-test'
                bat 'docker push nomathexpectation/teedy-test'
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
}
