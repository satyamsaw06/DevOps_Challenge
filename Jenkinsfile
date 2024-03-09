pipeline {
    agent any
    
    parameters {
        string(defaultValue: '/home/satyam/', description: 'Custom workspace path', name: 'customWorkspace')
    }
    
    stages {
        stage('Clone from GitHub') {
            steps {
                dir(params.customWorkspace) {
                    git url: 'https://github.com/satyamsaw06/DevOps_Challenge.git'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    dir(params.customWorkspace) {
                        docker.build('satyamsaw06/helloworld')
                    }
                }
            }
        }
        
        stage('Tag Docker Image') {
            steps {
                script {
                    docker.image('satyamsaw06/helloworld').tag('latest')
                }
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker') {
                    sh "docker push satyamsaw06/helloworld "
                }
                    }
                }
        stage('Creating deployement & used service nodeport ') {
            steps {
                script {
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'kubernetes', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://192.168.49.2:8443') {
                    sh "kubectl apply -f /home/satyam/deployement.yaml"
                    sh "kubectl apply -f /home/satyam/node-portservice.yaml"
                    sh "kubectl port-forward --address 0.0.0.0 svc/helloworld-service 30000:80" #used minikube, push forward 
}
                }
            }
        }
            }
        }
    }
    
    


