pipeline {
    
    agent any
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    } 
    
    stages {
        
        stage('Checkout'){
           steps {
                git credentialsId: 'w54t89e4-8g64-78r0-c39rt-rer57gt7f33', 
                url: 'https://github.com/ejejosh/cicd-python-jenkins-argocd-k8s',
                branch: 'main'
           }       
        }

        stage('Build Docker'){
            
            }   
        }

        stage('Push the artifacts'){
           
        }
        
        stage('Checkout K8S manifest SCM'){
            
        }
        
        stage('Update K8S manifest & push to Repo'){
            
        }
    }
}
