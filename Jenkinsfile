pipeline {

    agent any

    environment {
        DOCKERHUB_USER = "ditdevops1"
        BACKEND_IMAGE  = "backend-employe"
        FRONTEND_IMAGE = "frontend-employe"
        IMAGE_TAG      = "1.${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                sh """
                    docker build -t ${DOCKERHUB_USER}/${BACKEND_IMAGE}:${IMAGE_TAG} ./backend
                """
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh """
                    docker build -t ${DOCKERHUB_USER}/${FRONTEND_IMAGE}:${IMAGE_TAG} ./frontend
                """
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                        docker push "$DOCKERHUB_USER/$BACKEND_IMAGE:$IMAGE_TAG"

                        docker push "$DOCKERHUB_USER/$FRONTEND_IMAGE:$IMAGE_TAG"

                        docker logout
                    '''
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        success {
            echo "Déploiement Backend et Frontend Gestion Employé réussi !"
        }

        failure {
            echo "Le déploiement a échoué. Vérifiez les logs Jenkins."
        }
    }
}