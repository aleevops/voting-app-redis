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
              sh 'docker images -a'
              sh cd azure-vote
              sh 'ls -l'
              sh 'docker build -t jenkins-pipeline .'
              sh 'cd ..'
            }
        }
    }
}

