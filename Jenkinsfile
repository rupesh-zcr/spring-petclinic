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
                  sh 'docker build -t fleetapp .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                    aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 470447642752.dkr.ecr.ap-southeast-1.amazonaws.com
                    sh 'docker tag fleetapp:latest 470447642752.dkr.ecr.ap-southeast-1.amazonaws.com/fleetapp:latest'
                    sh 'docker push 470447642752.dkr.ecr.ap-southeast-1.amazonaws.com/fleetapp:latest'
                
            }
        }
    }
}
