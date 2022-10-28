pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    environment {
        DOCKER_TAG = getVersion()
    }

    stages{
        // stage("smc"){
        //     git 'https://github.com/thangSu/demo-asible-docker.git'
        // }    
        stage("maven build"){
            steps{
                dir('helloworld'){
                    sh 'mvn clean package'
                } 
            }
        }
        stage("docker build"){
            steps{
                dir('helloworld'){
                    sh 'docker build . -t thangsu/thangapp:${DOCKER_TAG}'
                } 
            }
        }
        stage("docker push"){
            steps{
                    withCredentials([string(credentialsId: 'docker-pass', variable: 'docker_password')]) {
                         sh "docker login -u thangsu -p ${docker_password}"
                    }   
                   
                    sh "docker push thangsu/thangapp:${DOCKER_TAG}"
            }
        }
        stage("ansible deploy"){
            steps{
                ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, extras: '-e DOCKER_TAG=${DOCKER_TAG}', installation: 'ansible', inventory: 'hosts', playbook: 'deploy-docker.yaml'
            }
        }
    }
    
}

def getVersion(){
    def commitHash = sh returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}