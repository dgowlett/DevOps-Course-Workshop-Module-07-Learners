pipeline {
    agent {
        docker { image 'node:17-bullseye' }
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
                dir('DotnetTemplate.Web') {
                sh "npm ci"
                sh "npm run build"
                }
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