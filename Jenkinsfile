pipeline {
    agent any

      tools {
        maven 'maven'
    }
    stages {
        stage('Build') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SelvaDev23/my-web-app.git']]])
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to K8s'){
            steps{
                script{
                    deploy adapters: [tomcat9(path: '', url: 'http://13.234.213.88:8080/')], contextPath: null, onFailure: false, war: '***/*.war'
                }
            }
        }
    
    }    
}
