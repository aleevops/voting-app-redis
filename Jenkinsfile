pipeline {
    agent any
    stages {
        stage('VerifyBranch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Git checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/aleevops/voting-app-redis.git']])
              }
          }
        stage('DockerImages'){
            steps {
              pwsh(script: 'docker images -a')
              pwsh(script: """
                cd azure-vote
                docker images -a
                docker build -t jenkins-pipeline .
                docker images -a
                cd ..
              """
              )
            }
        }
    }
}

