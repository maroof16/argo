pipeline {
    agent {
        docker {
            image 'maroofshaikh09/jenkinsagent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
    SONAR_URL = "http://65.2.38.167:9000"
    // DOCKER_IMAGE = "maroofshaikh09/argo-icd:{BUILD_NUMBER}"
    // REGISTRY_CREDENTIALS = credentials("docker-credential")
    GIT_REPO_NAME = "argo"
    GIT_USER_NAME = "maroof16"
    // user_email  = "maroofshaikh09@gmail.com"
    }
    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/maroof16/argo.git'
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
                    def dockerImage = docker.build("maroofshaikh09/argo-cicd:${env.BUILD_NUMBER}", ".")
                       withDockerRegistry(credentialsId: 'docker-credential') { 
                        dockerImage.push()
                    }
                }
            }
        }
        stage('update Deployment File'){
            steps {
                withCredentials([string(credentialsId: 'GITHUB_TOKEN', variable: 'GITHUB')]) {
                    sh '''
                        git config  user.email "maroofshaikh09@gmail.com"
                        git config user.name "maroofshaikh"
                        BUILD_NUMBER=${BUILD_NUMBER}
                        sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" deployment.yml
                        git add deployment.yml
                        git commit --message="Update Image Tag to version ${BUILD_NUMBER}"
                        git push https://${GITHUB}@github.com/${GIT_USER_NAME}/${GIT_USER_NAME} HEAD:main
                    '''
                }
            }   
        }
    }
}
 