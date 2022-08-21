pipeline {
    agent any
  stages {
    stage('Preparing Install') {
      steps {
        sh 'echo  install'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        //def customImage = docker.build("my-image:${env.BUILD_ID}")
        sh '/usr/local/bin/docker build -t chrome:${env.BUILD_ID}.'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        //withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        //  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
        //  sh 'docker push shanem/spring-petclinic:latest'
        sh 'echo pushed'
        //}
      }
    }
  }
}
