// pipeline {
//     agent {
//         docker {
//             image 'maroofshaikh09/docker-agent:latest'
//             args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
//     stages {
//         stage('git checkout') {
//             steps {
//                 sh "echo passwd"
//                 sh "git clone https://github.com/maroof16/argo.git"
//             }
//         }
//     }
// }
pipeline {
    agent {
        docker { image 'node:18.17.1-alpine3.18' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
