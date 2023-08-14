pipeline {
    agent {
        docker {
            image 'maroofshaikh09/jenkinsagent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
    SONAR_URL = "http://13.233.196.5:9000"
    // DOCKER_IMAGE = "maroofshaikh09/argo-icd:{BUILD_NUMBER}"
    // REGISTRY_CREDENTIALS = credentials("docker-credential")
    }
    stages {
        stage('git checkout') {
            steps {
                 git branch: 'main', url:'https://github.com/sahill20/java-maven-sonar-argocd-helm-k8s.git'
            }
        }
        stage("Build and test") {
            steps {
                sh 'mvn -X clean package'
            }
        }
        stage ("static code analysis") {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'sonar')]) {
                    sh 'mvn sonar:sonar -Dsonar.login=$sonar -Dsonar.host.url=${SONAR_URL}'
                }
            }
        }
        stage ('Build And Push') {
            steps {
                script {
                    // sh ' docker build -t ${DOCKER_IMAGE} . '
                    // def dockerImage = docker.image{"${DOCKER_IMAGE}"}
                    // docker.withRegistry('https://index.docker.io/v1/',"${REGISTRY_CREDENTIALS}") {
                    // dockerImage.push()
                    def dockerImage = docker.build("maroofshaikh09/argo-icd:${env.BUILD_NUMBER}", ".")
                       withDockerRegistry(credentialsId: 'docker-credential') { 
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
 