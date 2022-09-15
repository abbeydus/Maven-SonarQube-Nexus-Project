pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/abbeydus/Maven-project.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('codequality'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=sonar-abbeypipeline \
  -Dsonar.host.url=http://ec2-3-130-66-7.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.login=sqp_65a0256a8ca1648c5e96abd08f39178c0091414e'
      }
    }
  }
}