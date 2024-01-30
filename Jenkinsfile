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
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t ejejosh/tan_demo:${BUILD_NUMBER} .
                    '''
                }          
            }   
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push ejejosh/tan_demo:${BUILD_NUMBER}
                    '''
                }
            }
           
        }
        
        stage('Checkout K8S manifest SCM'){
            steps {
                git credentialsId: 'w54t89e4-8g64-78r0-c39rt-rer57igt733', 
                url: 'https://github.com/ejejosh/cicd-k8s-manifest-repo.git',
                branch: 'main'
            }
 
        }
        
        stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                    withCredentials([usernamePassword(credentialsId: 'w54t89e4-8g64-78r0-c39rt-rer57igt733', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh '''
                        cat deploy.yaml
                        sed -i '' "s/32/${BUILD_NUMBER}/g" deploy.yaml
                        cat deploy.yaml
                        git add deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push https://github.com/ejejosh/cicd-k8s-manifest-repo.git HEAD:main
                        '''                        
                    }
                }
            }
            
        }
    }
}
