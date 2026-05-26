pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Code récupéré depuis GitHub'
            }
        }
        stage('Build') {
            steps {
                echo 'Build de l image Docker'
                sh 'docker build -t mon-app:latest .'
            }
        }
        stage('Test') {
            steps {
                echo 'Lancement des tests'
                sh 'docker run --rm mon-app:latest npm test'
            }
        }
    }
    post {
        success { echo 'Pipeline réussi !' }
        failure { echo 'Pipeline en échec !' }
    }
}