pipeline {
    agent any
    
    tools {
        // Ensure the Sonar Scanner is available
        sonarQubeScanner 'SonarScanner'
    }
    
    environment {
        // Use the configured SonarQube instance name
        SONARQUBE = 'MySonarQube'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/deopura/getting-started.git'
          }
        }

        stage('Build') {
            steps {
                echo 'Building..'
                // Check the docker-compose version
                sh 'docker compose version'
                // Bring up the services
                sh 'docker compose up -d'               // Ensure the services are running
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker compose ps'
            }
        }
    }
}
