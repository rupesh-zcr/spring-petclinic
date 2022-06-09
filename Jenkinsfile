pipeline{
    agent any
    
    stages {
        stage('Build Maven') {
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'githubpwd', url: 'https://github.com/rupesh-zcr/spring-petclinic.git']]])           
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t java-docker/my-app-2.0 .'
                }
            }
        }
        
    }
}
