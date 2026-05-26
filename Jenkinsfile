pipeline {
    agent any
    environment {
        IMAGE_NAME = 'mon-app'
        IMAGE_TAG  = "${BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Récupération du code - Build #${BUILD_NUMBER}"
            }
        }
        stage('Build Docker') {
            steps {
                echo 'Construction de l image Docker...'
                bat 'docker build -t mon-app:%BUILD_NUMBER% .'
            }
        }
        stage('Test') {
            steps {
                echo 'Lancement des tests...'
                bat 'docker run --rm mon-app:%BUILD_NUMBER% npm test'
            }
        }
        stage('Deploy Staging') {
            steps {
                echo 'Déploiement sur Staging...'
                bat 'docker stop staging-app || exit 0'
                bat 'docker rm staging-app || exit 0'
                bat 'docker run -d --name staging-app -p 3001:3000 mon-app:%BUILD_NUMBER%'
                echo 'Application disponible sur http://localhost:3001'
            }
        }
    }
    post {
        success { echo 'Pipeline réussi ! Application déployée sur staging.' }
        failure { echo 'Pipeline en échec - vérifiez les logs.' }
    }
}
