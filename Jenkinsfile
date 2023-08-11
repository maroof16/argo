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
// pipeline {
//     agent {
//         docker { image 'node:18.17.1-alpine3.18' }
//     }
//     stages {
//         stage('Test') {
//             steps {
//                 sh 'node --version'
//             }
//         }
//     }
// }
pipeline {
    agent none
    stages {
        stage('Back-end') {
            agent {
                docker { image 'maven:3.9.3-eclipse-temurin-17-alpine' }
            }
            steps {
                sh 'mvn --version'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:18.17.1-alpine3.18' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}