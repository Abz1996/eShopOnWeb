pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dotnet-architecture/eShopOnWeb.git'
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
            cleanWs()
        }
    }
}
