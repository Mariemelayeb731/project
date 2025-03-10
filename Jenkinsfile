pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mariemelayeb731/project:latest'
    }

    stages {
        stage('Cloner le projet') {
            steps {
                git 'https://github.com/Mariemelayeb731/project.git'
            }
        }

        stage('Construire l’application') {
            steps {
                sh './mvnw clean package' // Backend Spring Boot
                sh 'npm install && npm run build' // Frontend Angular
            }
        }

        stage('Tests') {
            steps {
                sh './mvnw test' // Tests backend
                sh 'npm test'    // Tests frontend
            }
        }

        stage('Construire et Pousser l’image Docker') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Déployer sur le serveur') {
            steps {
                sshagent(['serveur-ssh']) {
                    sh 'ssh user@server "docker pull $DOCKER_IMAGE && docker-compose up -d"'
                }
            }
        }
        stage('Tests Backend (JUnit)') {
            steps {
                script {
            // Exécuter les tests unitaires Spring Boot avec Maven
                     sh './mvnw clean test'
                }
             } 
        }
        stage('Tests Frontend (Karma/Jasmine)') {
            steps {
                script {
            // Exécuter les tests unitaires Angular avec Karma
                     sh 'npm install'
                     sh 'npm run test -- --watch=false --browsers=ChromeHeadless'
                }
            } 
        }
        stage('Tests d\'intégration') {
            steps {
                script {
            // Exécuter les tests d'intégration Spring Boot avec Testcontainers
                    sh './mvnw clean verify'  // La phase 'verify' inclut les tests d'intégration
                }
            }
        }
        stage('Tests End-to-End (Cypress)') {
            steps {
                script {
            // Exécuter les tests end-to-end avec Cypress
                    sh 'npm install'
                    sh './node_modules/.bin/cypress run'
                }
            }
        }



    }
}
