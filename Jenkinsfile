pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "web-production"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('web') {
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
        container('maven') {
          dir('web') {
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
