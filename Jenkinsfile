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
                sh 'dotnet test'
                }
                dir('DonetTemplate.Web.Tests') {
                sh "npm ci"
                sh "npm run build"
                }
            }
        }
        stage('Test') {
            steps {
 
                dir('DotnetTemplate.Web') {
                               echo 'Testing npm TypeScript tests..'
                sh "npm t"
                               echo 'Testing npm linting on the TypeScript..'
                sh "npm run lint"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}