pipeline {
    agent {
        docker{
          image 'maroofshaikh09/docker-agent:latest'
          args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages{
        stage('git checkout'){
            steps{
                sh "echo passwd"
                git 'https://github.com/maroof16/argo.git'
            }
        }
    }
}