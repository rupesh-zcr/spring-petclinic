pipeline{
    agent any
    
    stages {
        stage('Build Maven') {
            steps{
               sh 'git clone https://github.com/rupesh-zcr/spring-petclinic.git'           
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t demo/test .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 992022947233.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker tag demo/test:latest 992022947233.dkr.ecr.ap-south-1.amazonaws.com/demo/test:latest'
                    sh 'docker push 992022947233.dkr.ecr.ap-south-1.amazonaws.com/demo/test:latest'
                }
            }
        }
    }
}
