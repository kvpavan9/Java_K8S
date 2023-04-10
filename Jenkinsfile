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
        
       stage('Deploying App to Kubernetes') {
         steps {
           script {
              kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
