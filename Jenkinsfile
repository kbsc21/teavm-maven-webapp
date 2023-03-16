pipeline {
agent any
  //agent {
  //label 'jenkins_slave'
//}
  stages {
  stage('Checkout') {
    steps {
      checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']])
    }
  }
     stage('Build') {
       when {
  branch 'PR1'
}
    steps {
      sh 'mvn compile'
    }
  }
     stage('Test') {
          when {
  branch 'PR1'
}
    steps {
      sh 'mvn test'
    }
  }
   /*   stage('Deploy') {
    steps {
      sshagent(['tomcat_deploy']) {
    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/teavm-maven-webapp-pipeline/target/teavm-maven-webapp-1.0-SNAPSHOT.war ubuntu@172.31.9.172:/opt/tomcat/webapps'
}
    }
  } */
     stage('Notify') {
      steps {
          slackSend channel: '#devopsdeepdive_batch14', message: 'message: "Build Started: ${env.JOB_NAME}'
      }
  }

}

}
