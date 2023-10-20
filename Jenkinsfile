pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SelvaDev23/devOpsWeb.git']]])
                sh 'mvn clean package'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t iamselva/My-Web-App .'
                }
            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                     // some block
                    }
                    sh 'docker login -u iamselva -p ${dockerhubpwd}'

                    sh 'docker push iamselva/My-Web-App'
                }
            }
        }  
    }
}          
