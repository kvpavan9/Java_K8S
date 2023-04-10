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
                    sh 'docker build -t smondepulanka/helloworld .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   sh 'docker login -u smondepulanka -p P@andurga541541'

                   sh 'docker push smondepulanka/helloworld'
                }
            }
        }
stage('Integrate Jenkins with EKS Cluster and Deploy App') {
            steps {
                withAWS(credentials: '951664088898', region: 'us-east-1') {
                  script {
                    sh ('aws eks update-kubeconfig --name demo-eks --region us-east-1')
                    sh "kubectl apply -f deployment.yml"
                }
                }
        }
    }
    }
}
