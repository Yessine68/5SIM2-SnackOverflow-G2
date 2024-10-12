pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Récupération du code') {
            steps {
                git 'https://github.com/Yessine68/5SIM2-SnackOverflow-G2.git'
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