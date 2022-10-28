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
                    sh 'docker build -t thangsu/thangapp:${DOCKER_TAG}'
                } 
            }
        }
    }
    
}

def getVersion(){
    def commitHash = sh returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}