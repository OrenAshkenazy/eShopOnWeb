def loadProperties() {
    node {
        checkout scm
        properties = new Properties()
        File propertiesFile = new File("${workspace}/pipeline.properties")
        properties.load(propertiesFile.newDataInputStream())
        echo "Immediate one ${properties.repo}"
    }
}

pipeline {
    agent any

    stages {
        stage('Init WS') {
            steps{
                script{
                   step([$class : 'GitHubPRStatusBuilder', statusMessage: [content: "Run #${env.BUILD_NUMBER} started"]])
                 //  setGitHubPullRequestStatus context: '', message: '', state: 'PENDING'
                    
                  }
            }
        }

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
