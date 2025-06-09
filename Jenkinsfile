pipeline {
    agent any

    environment {
        DOTNET_ROOT = "/usr/share/dotnet"
        PATH = "${DOTNET_ROOT}:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abz1996/eShopOnWeb.git'
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore src/Web/Web.csproj'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build src/Web/Web.csproj --configuration Release --no-restore'
            }
        }

        stage('Test') {
            steps {
                // Optionally specify the actual test project if needed
                sh 'dotnet test --no-restore --no-build'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish src/Web/Web.csproj --configuration Release --output publish --no-restore --no-build'
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
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
