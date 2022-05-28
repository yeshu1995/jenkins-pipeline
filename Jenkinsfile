pipeline {
    environment {
        registry = "yasoda123/Yeshu"
        registryCredential = 'Docker_Id'
    }
    agent any
    stages {
        stage('Checkout') {
            steps {
                     // Get code from a GitHub repository
                    git url:'https://github.com/Raviteja1775/git.git', branch: 'main',
                    credentialsId: 'Git'
            }
        }
        stage('Building image') {
            steps{
                sh 'docker build -t jenkintest:latest .'
                  sh 'docker tag jenkintest yasoda123/jenkintest:latest'
                sh 'docker tag jenkintest yasoda123/jenkintest:$BUILD_NUMBER'
            }
        }
        stage('Deploy our image') {
            steps {
                withDockerRegistry([ credentialsId: "Docker_Id", url: "" ]) {
              sh  'docker push yasoda123/jenkintest:latest'
              sh  'docker push yasoda123/jenkintest:$BUILD_NUMBER'
                }
            }
        }
    }
}
