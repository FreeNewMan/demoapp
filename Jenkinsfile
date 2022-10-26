pipeline {
  environment {
    registry = "lutovp/demoapp"
    registryCredential = 'dockerhub'
  }
  
  agent any
  
  parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'main', name: 'BRANCH', type: 'PT_BRANCH'
  }
  
  stages {
      
    stage('Set Branch') {
      steps {
        git branch: "${params.BRANCH}", url: 'https://github.com/FreeNewMan/demoapp.git'
      }
    }
    
    
    stage('Cloning Git') {
      steps {
        git 'https://github.com/FreeNewMan/demoapp.git'
      }
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