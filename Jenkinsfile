pipeline {
    agent any
    stages {
        stage('VerifyBranch') {
            steps {
                echo "$GIT_BRANCH"
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

