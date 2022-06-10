pipeline{
    
    environment {
        CLUSTER_NAME="non-prd-eks1"
        EKS_CLUSTER_CURRENT_CONTEXT_NAME="arn:aws:eks:ap-south-1:992022947233:cluster/${CLUSTER_NAME}"
        NAMESPACE="test"
        
    }
        
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
        stage('Deploy'){
            steps {
                 sh ''' 
                   aws eks update-kubeconfig --name $CLUSTER_NAME --region ap-south-1
                   kubectl config use-context $EKS_CLUSTER_CURRENT_CONTEXT_NAME
                   kubectl get ns
                   '''
            }
        }
        
    }
}
