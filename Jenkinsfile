pipeline {
    agent any

    environment {
        DOTNET_ROOT = "/usr/share/dotnet"  // Adjust this if your agent uses Windows
        PATH = "${env.DOTNET_ROOT}:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abz1996/eShopOnWeb.git'
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore src/Web/BlazorShared/BlazorShared.csproj'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build src/Web/BlazorShared/BlazorShared.csproj --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish src/Web/BlazorShared/BlazorShared.csproj -c Release -o ./publish'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'publish/**', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
    }
}
