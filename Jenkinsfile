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
        sh """
            /bin/docker build --network=host -t nginx:${env.BUILD_ID} .
        """
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        //withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        //  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
        //  sh 'docker push shanem/spring-petclinic:latest'
        sh """
            /usr/bin/aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 171109243224.dkr.ecr.ap-southeast-1.amazonaws.com
            /bin/docker tag nginx:${env.BUILD_ID} 171109243224.dkr.ecr.ap-southeast-1.amazonaws.com/testrepo1:${env.BUILD_ID}
            /bin/docker push 171109243224.dkr.ecr.ap-southeast-1.amazonaws.com/testrepo1:${env.BUILD_ID}
            echo 'Image Pushed to Registry'
        """
        //}
      }
    }
      stage('Deploy approval'){
          steps{
            input "Deploy to kubernetes?"
          }
      }
      stage('K8S Deployment') {
          steps{
          sh"""
            /usr/local/bin/kubectl get po -A
            /usr/local/bin/kubectl set image deployment/nginx-deployment nginx-deployment=171109243224.dkr.ecr.ap-southeast-1.amazonaws.com/testrepo1:${env.BUILD_ID}
            
          """
          }
      }
  }
}
