pipeline{
    agent any
    stages{
        // stage("smc"){
        //     git 'https://github.com/thangSu/demo-asible-docker.git'
        // }

    tools{
        maven 'maven3'
    }
    }
    stage("maven build"){
        steps{
            dir('helloworld'){
                 sh 'mvn clean package'
            } 
        }
    }
}