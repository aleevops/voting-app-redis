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
              sh '''docker images -a
                    cd azure-vote
                    ls -l
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                    pwd
                    ls -l
                    '''
            }
        }
        stage('Start Test app'){
          steps{
            sh 'docker-compose up -d'
            sh "chmod +x -R ${env.WORKSPACE}"
            sh './scripts/test_container.sh'  
          }
          post{
            success{
              echo "App Started successfully"
            }
            failure{
              echo "App failed to start"
            }
          }
        }
        stage('Run Tests'){
          steps{
            sh 'pytest ./tests/test_sample.py'
          }
        }
        stage('Stop Test App'){
          steps{
              sh 'docker-compose down'
          }
        }
    }
}

