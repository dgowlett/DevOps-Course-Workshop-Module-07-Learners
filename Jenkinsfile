#docker { image 'node:17-bullseye' }

pipeline {
    agent {
        docker { image 'mono:latest' }
    }
    environment {
            DOTNET_CLI_HOME = '/tmp/dornet_cli_home'
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
                sh 'dotnet build'
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