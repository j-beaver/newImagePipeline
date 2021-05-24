pipeline {
  environment {
    imagename = "test_image"
    registry = 'http://localhost:8083'
  }
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build(imagename)
                }
                sh 'echo BUILD SUCCESSFULL '
                
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside(){
                        sh 'echo TEST WITHIN'
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry(registry, 'dockerUserCreds'){
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
