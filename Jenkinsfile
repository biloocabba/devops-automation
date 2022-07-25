pipeline{
    agent any
    tools{
        maven 'maven-3.8.4'
    }
    stages{
        stage("Build maven"){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/biloocabba/devops-automation.git']]])
                sh 'mvn clean install'
            }
        }
        stage("Build Docker image"){
            steps{
                script{
                    sh 'docker build -t biloocabba/devops-automation . '
                    
                }
                
            }
        }
        stage("Push Docker image to hub"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                    sh 'docker login -u biloocabba -p ${dockerhub}'    
                    sh 'docker push biloocabba/devops-automation:latest'    
                    }
                    
                }
                
            }
        }
    }
}
