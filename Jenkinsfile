pipeline {
    agent none
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
                sh 'cd DotnetTemplate.Web/'
                sh 'npm install'
                sh 'npm run build'
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
                sh 'cd DotnetTemplate.Web/'
                sh 'npm t'
                sh 'npm run lint'
            }
        
    }
}