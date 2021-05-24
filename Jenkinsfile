pipeline {
  environment {
    imagesuffix = "-custom"
    registry = 'localhost:8083'
    registryurl = 'http://localhost:8083'
    dockerfile = "Dockerfile"
  }
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo UPDATE DOCKER FILE WITH THE PIPELINE INPUTS'
                script {
                    def text = readFile dockerfile
                    text = text.replaceAll("registry", env.registry).replaceAll("image", env.image).replaceAll("tag", env.tag)
                    writeFile file: "Dockerfile", text: text

                    def imageCustomName = env.image + env.imagesuffix + ":" + env.tag
                    dockerImage = docker.build(imageCustomName)
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
                    docker.withRegistry(registryurl, 'dockerUserCreds'){
                        dockerImage.push()
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
