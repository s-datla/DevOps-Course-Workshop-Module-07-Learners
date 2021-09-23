pipeline {
    agent none
    environment {
        DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
    }
    stages {
        stage('DotNet Build') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('Node install and build') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                dir('DotnetTemplate.Web'){
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('DotNet Test') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            steps {
                sh 'dotnet test'
            }
        }
        stage('Node test and lint') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                dir('DotnetTemplate.Web'){
                    sh 'npm run test-with-coverage'
                    sh 'npm run lint'
                    publishCoverage adapters: [istanbulCoberturaAdapter('/coverage/cobertura-coverage.xml')]
                }
            }
        }
        
    }
}