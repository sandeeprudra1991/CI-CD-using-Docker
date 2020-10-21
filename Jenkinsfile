pipeline {
    agent any
    environment
     {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        IMAGE = "$PROJECT:$VERSION"
        registry = "123456nish/spring"
        registryCredential = 'docker'
        dockerImage = ''
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Nishanth-ctrl/CI-CD-using-Docker.git'
             
          }
        }
        
      stage('Image Build'){
           steps{
               script{
                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
             }
         }
      stage('Deploy our image') {
          steps{
            script {
              docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
            }
        }
            }
        }
      stage('docker-compose') {
          steps {
             sh "docker-compose build"
             sh "docker-compose up -d"
          }
      }	
}         
}
