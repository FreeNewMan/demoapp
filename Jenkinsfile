pipeline {
  environment {
    registry = "lutovp/demoapp"
    registryCredential = 'dockerhub'
  }
  
  agent any
 
  
  stages {
      
    stage("Git checkout"){
        git credentialsId: 'f7a92abb-51aa-48ea-8b25-b7b36a52f411', url: 'git@github.com:FreeNewMan/demoapp.git'
    }
    stage("Sample define secret_check"){
        secret_check=true
    }
      
     
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    
     stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }   
  }
}