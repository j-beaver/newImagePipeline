pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                sh 'echo "Hello World"'
                sh 'touch /tmp/test.msg'
            }
        }
        stage('test') {
            steps {
                sh 'echo "Hello Test World"'
                sh 'touch /tmp/test.msg'
            }            
        }
    }
}
