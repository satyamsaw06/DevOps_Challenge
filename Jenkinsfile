pipeline {
    agent any
    
    parameters {
        string(defaultValue: '/mnt/devopschallenge', description: 'Custom workspace path', name: 'customWorkspace')
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
            }
        }
    }
    
    


