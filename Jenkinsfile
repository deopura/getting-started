pipeline {
    agent any

    environment {
        SONAR_HOST = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarqubetoken')  // Uses Jenkins credentials securely
    }

    tools {
        // Declare SonarScanner to simplify later access
        sonarScanner 'SonarScanner'
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()  // Cleans workspace before pipeline starts
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/deopura/getting-started.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=sonartest \
                        -Dsonar.sources=src \
                        -Dsonar.host.url=${SONAR_HOST} \
                        -Dsonar.login=${SONAR_TOKEN}
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'docker compose version'
                // Optional: bring up services if needed
                // sh 'docker compose up -d'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Insert your test command here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'docker compose ps'
            }
        }
    }

    
}
