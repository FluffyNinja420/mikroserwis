pipeline {
  agent {
    node {
      label 'node 7'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t mikroserwis/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t mikroserwis/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t mikroserwis/worker ./worker'
      }
    }
    stage('Push result image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'https://index.docker.io/v1/') {
          sh 'docker push mikroserwis/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'https://index.docker.io/v1/') {
          sh 'docker push mikroserwis/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'https://index.docker.io/v1/') {
          sh 'docker push mikroserwis/worker'
        }
      }
    }
  }
}
