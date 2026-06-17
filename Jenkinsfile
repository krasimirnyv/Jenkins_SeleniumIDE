pipeline {
    agent any

    environment {
        PATH = "/usr/local/share/dotnet:${env.PATH}"
    }

    stages {
        stage("Restore Packages"){
            steps {
                sh 'dotnet restore'
            }
        }
        stage("Build Project"){
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        stage("Run Tests"){
            steps {
                sh 'dotnet test --no-build --logger "trx" --results-directory TestResults'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
        }
    }
}