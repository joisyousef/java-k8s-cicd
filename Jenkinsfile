pipeline {
    agent {
        label "jenkins-agent"
    }
    tools {
        jdk 'Java21'
        maven 'Maven3'
    }
    environment{
        APP_NAME = "java-k8s-cicd"
        RELEASE = "1.0.0"
        DOCKER_USER = "joisyousef"
        DOCKER_PASS = "docker-hub-credentials"
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}" 
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
                withSonarQubeEnv(installationName: 'sonarqube-scanner', credentialsId: 'jenkins-sonar-token') {              
                    sh 'mvn sonar:sonar'
                }
            }   
        }
          stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }

        }
    }                               
}
