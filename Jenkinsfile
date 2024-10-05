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
        stage('Checkout from SCM') {
            steps {
                git branch: 'main', credentialsId: 'Github-Token', url: 'https://github.com/joisyousef/java-k8s-cicd.git'
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
                      withSonarQubeEnv(credentialsId: 'jenkins-sonar-token') {              
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
