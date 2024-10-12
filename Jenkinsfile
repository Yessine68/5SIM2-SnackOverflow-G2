pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    environment {
        DOCKER_IMAGE = "yessine68/5sim2-snackoverflow-g2"
        DOCKER_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Récupération du code') {
            steps {
                git branch: 'main', url: 'https://github.com/yessine68/5SIM2-SnackOverflow-G2.git'
            }
        }
        
        stage('Nettoyage') {
            steps {
                sh 'mvn clean'
            }
        }
        
        stage('Construction') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        
        stage('Construction Image Docker') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }
        
        stage('Push Image Docker') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push("latest")
                    }
                }
            }
        }
        
        stage('Déploiement') {
            steps {
                echo "Déploiement de l'image ${DOCKER_IMAGE}:${DOCKER_TAG}"
            }
        }
    }
}