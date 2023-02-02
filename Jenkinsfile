pipeline {
agent any
stages {
  stage('Checkout') {
    steps {
      checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-user', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']])
    }
  }
  stage('Build') {
    steps {
     sh 'mvn compile'
    }
  }
  // stage('Test') {
   // steps {
    // sh 'mvn test'
    //}
  //}
   stage('Package') {
    steps {
     sh 'mvn package'
    }
  }
 stage('Deploy') {
    steps {
    sshagent(['tomcat_server']) {
    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/teavm-maven-webapp/target/teavm-maven-webapp-1.0-RELEASE.war ubuntu@172.31.7.90:/opt/tomcat/webapps'
}
    }
  }
}
}
