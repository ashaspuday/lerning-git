pipeline {
  environment {
    imagename = "ashaspuday/mynginxapp"
    registryCredential = 'dockerid'
    dockerImage = ''
    }
    agent any
    stages {
        stage('Git Clone') {
            steps {
                git([url: 'https://github.com/wo7and/lerning-git.git', branch: 'master', credentialsId: 'git-token'])
            }
        }
        stage('Build Image') {
            steps {
               script {
                 dockerImage = docker.build imagename
               }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                  docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                  }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps {
              sh "docker rmi $imagename:$BUILD_NUMBER"
             }
        }
    }
}
