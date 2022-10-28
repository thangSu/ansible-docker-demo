pipeline{
    agent any
    tools{
        maven 'maven3'
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
    }
    
}