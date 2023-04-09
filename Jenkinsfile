pipeline {
    agent any
     tools {
    maven 'Maven'
  }
    
    stages{
        stage('Build Maven'){
          steps{
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t helloworld .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   sh 'docker login -u smondepulanka -p P@andurga541541'

                   sh 'docker push helloworld:latest'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
    }
}
