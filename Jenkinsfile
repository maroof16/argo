// pipeline {
//     // agent {
//     //     docker {
//     //         image 'maroofshaikh09/agent:latest'
//     //         args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
//     //     }
//     // }
//     agent any
//     tools {
//         maven 'maven3'
//         jdk 'jdk11'
//     }
//     stages {
//         stage('git checkout') {
//             steps {
//                 git 'https://github.com/maroof16/argo.git'
//             }
//         }
//         stage("Build and test") {
//             steps {
//                 sh 'mvn -X clean package'
//             }
//         }
//         stage ("static code analysis") {
//             steps {
//                 withCredentials([string(credentialsId: 'sonar-token', variable: 'sonar')]) {
//                     sh 'mvn sonar:sonar -Dsonar.login=$sonar -Dsonar.host.url= http://13.235.246.22:9000'
//                 }
//             }
//         }
//         stage ('Build And Push') {
//             steps {
//                 script {
//                     withDockerRegistry(credentialsId: 'docker-id-pass') {
//                     sh """ docker build -t image .
//                     docker tag  image maroofshaikh09/argocd-demo:$BUILD
//                     docker push   maroofshaikh09/argocd-demo:$BUILD
//                     """
//                     }
//                 }
//             }
//         }
//     }
// }
pipeline {
    agent any 
    
    tools{
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/jaiswaladi246/Petclinic.git'
            }
        }
        
//         stage("Compile"){
//             steps{
//                 sh "mvn clean compile"
//             }
//         }
        
//          stage("Test Cases"){
//             steps{
//                 sh "mvn test"
//             }
//         }
//     }
// }