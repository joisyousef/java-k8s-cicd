pipeline {
  agent {
    label "jenkins-agent"
  }
  tools {
    jdk 'Java21'
    maven 'Maven3'
  }
  stages {
    stage('Cleanup Workspace') {
      steps {
        cleanWs()
      }
    }
    stage('Configure Git') {
      steps {
        sh 'git config --global http.postBuffer 524288000'
      }
    }
    stage('Checkout from SCM') {
      steps {
        git branch: 'main', credentialsId: 'Github-Token', url: 'https://github.com/joisyousef/java-k8s-cicd'
      }
    }
    stage('Build Stage') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Test Stage') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Sonarqube Analysis') {
      steps {
        withSonarQubeEnv(credentialsID:'jenkins-sonarqube-token') { // Replace 'SonarQube' with your actual installation name
          sh 'mvn sonar:sonar'
        }
      }
    }
  }
}
