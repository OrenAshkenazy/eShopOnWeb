pipeline {
    agent any

    stages {
        stage('restore') {
            steps {
               bat 'dotnet restore'
            }
        }
        stage('build') {
            steps {
               bat 'dotnet publish -c Release -o out'
            }
        }
        stage('pack') {
            steps {
                bat 'dotnet pack --no-build --output nupkgs'
            }
        }
    }
}
