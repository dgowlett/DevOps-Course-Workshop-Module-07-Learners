pipeline {
    agent {
        docker { image 'mcr.microsoft.com/dotnet/sdk:6.0' }
    }


    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout..'
                checkout scm
            }
        }
        stage('Build dotnet') {
            environment {
                DOTNET_CLI_HOME = '/tmp/dornet_cli_home'
            }
            steps {
                echo 'Building dotnet..'

                dir('DotnetTemplate.Web') {
                sh 'dotnet build'
                sh 'dotnet test'
                }
            }
        }
        stage('build npm') {
            steps {
                echo 'Building npm..'
        
                dir('DotnetTemplate.Web') {
                sh "pwd"
                sh "env"
                sh "ls -l"
                sh "apt install npm"
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
