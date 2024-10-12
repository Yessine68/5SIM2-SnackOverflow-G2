pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Récupération du code') {
            steps {
                git branch: 'main', url: 'https://github.com/Yessine68/5SIM2-SnackOverflow-G2.git'
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
    }
}