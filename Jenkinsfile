pipeline {
    agent any
    stages {
       stage('build') {
          steps {
             echo 'Notify GitLab'
             updateGitlabCommitStatus name: 'build', state: 'pending'
             echo 'build step goes here'
             updateGitlabCommitStatus name: 'build', state: 'success'
          }
       }
       stage(test) {
           steps {
               echo 'Notify GitLab'
               updateGitlabCommitStatus name: 'test', state: 'pending'
               echo 'test step goes here'
               updateGitlabCommitStatus name: 'test', state: 'success'

           }
       }
       stage(deploy) {
           steps {
               echo 'Notify GitLab'
               updateGitlabCommitStatus name: 'deploy', state: 'pending'
               echo 'Deploy step goes here'
               updateGitlabCommitStatus name: 'deploy', state: 'success'

           }
       }
    }
 }
