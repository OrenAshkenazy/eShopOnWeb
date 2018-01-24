def loadProperties() {
        properties = new Properties()
        File propertiesFile = new File("${workspace}/pipeline.properties")
        properties.load(propertiesFile.newDataInputStream())
}

pipeline {
    agent any

    stages {
        stage('Init WS') {
            steps{
                script{
                    def props = readProperties  file:"${workspace}/pipeline.properties"
                    def Var1 = props['version']
                    echo "Version: ${Var1}"
                    def Address = props['address']
                    def values = Address.split(';')
                        
                      //  for (i = 0; i < values.size(); i++){
                       //        echo value[i];
                       // }
                        
                        
                  //  loadProperties()
                  // echo "Later one ${properties.version}"
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
