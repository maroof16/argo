pipeline {
    agent {
        label 'docker-slave'
            // image 'maroofshaikh09/docker-agent:latest'
            // args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
    }
    stages {
        stage('git checkout') {
            steps {
                sh "echo passwd"
                sh "git clone https://github.com/maroof16/argo.git"
            }
        }
    }
}
