pipeline {
    agent any
    environment {
        dockerimage =''
        registry = 'rohanraga/jen-docker:2.0'
        
    }
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/999Rohan/JD.git']]])
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    dockerimage = docker.build registry
                }
            }
        }
        stage ('uploading image') {
            steps {
                script {
                        docker.withRegistry( '', 'rohanraga-docker' ) {
                        dockerimage.push()
                    }    
                }
            }
        }
		stage ('Docker Run') {
			steps {
				script {
					dockerimage.run("-p 8088:8080 --name jen2-dockercontainer1")
				}
			}
		}	
    }
}
