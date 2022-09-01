pipeline {
    agent none

    stages {

        stage('checkout') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:6.0' }
            }
            steps {
                echo 'Checkout..'
                checkout scm
            }
        }
        stage('Build dotnet') {
            
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:6.0' }
            }
            environment {
                DOTNET_CLI_HOME = '/tmp/dornet_cli_home'
            }
            stages {
                stage('Build dotnet') {
                    steps {
                        echo 'Building dotnet..'
                        dir('DotnetTemplate.Web') {
                            sh 'dotnet build'
                        }
                    }
                }
                stage('Test dotnet') {
                        steps {
                            echo 'test dotnet..'
                            dir('DotnetTemplate.Web') {
                                sh 'dotnet test'
                            }
                        }

                }
            }
        }

        stage('build npm') {

            agent {
                docker { image 'node:17-bullseye' }
            }
        
            steps {
                    echo 'Building npm..'
                    dir('DotnetTemplate.Web') {
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




    }
}
