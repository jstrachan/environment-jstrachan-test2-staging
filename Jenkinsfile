pipeline {
  agent {
    label "jenkins-jx-base"
  }
  environment {
    DEPLOY_NAMESPACE = "jx-staging"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('jx-base') {
          dir('env') {
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('jx-base') {
          dir('env') {
            sh 'jx step helm version'
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
