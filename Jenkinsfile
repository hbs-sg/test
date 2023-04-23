pipeline {
    agent any
    stages {
        stage('Docker version') {
            steps {
                sh '''
                    echo $USER
                    docker version
                '''
            }
        }
        stage('Build docker image') {
            steps {
                sh '''
                    docker build -t juliaboykowa/jenkins:latest .
                '''
            }
        }
        stage('Push docker image to DockerHub') {
            steps{
                withDockerRegistry(credentialsId: 'DockerHub', url: 'https://index.docker.io/v1/') {
                    sh '''
                        docker push juliaboykowa/jenkins:latest
                    '''
                }
            }
        }
        stage('Docker delete local image') {
            steps {
                sh '''
                    docker rmi juliaboykowa/jenkins:latest
                '''
            }
        }
    }
}
