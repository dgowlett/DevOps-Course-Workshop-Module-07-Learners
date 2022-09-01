pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout..'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh "npm ci"
                sh "npm run build"
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
            }
        }
    }
}