//declarative pipeline
pipeline{
  agent any  
  tools {
    maven "maven3.8.4"
  }
  triggers {
  pollSCM '* * * * * '
}
  stages {
    stage('1.CodeClone'){
      steps{
          git branch: 'master', url: 'https://github.com/sikwitit1/web-app'
      }
    } 
    stage('2.mavenBuild'){
      steps{
      sh "mvn clean package"
      } 
    }
    stage('3.CodeQuality') {
      steps{
      sh "echo reports done"
      //sh "mvn sonar:sonar"
      } 
    }
    stage('4.uploadToNexus'){
      steps{
      sh "echo artifacts uploaded"
      //sh "mvn deploy"
      } 
    }
    stage('5.Deploy2Tomcat'){
    steps{
    sshagent(['agent2']) {
    sh "scp -o StrictHostKeyChecking=no target/*war ec2-user@172.31.14.229:/opt/tomcat9/webapps
}
    
} 
    }
    }
  post{
    always {
     mail bcc: 'ja4prezz@gmail.com', body: '''Build complete 

Landmark Technologies''', cc: 'ja4prezz@gmail.com', from: '', replyTo: '', subject: 'Build done', to: 'ja4prezz@gmail.com'
    } 
    failure {
    mail bcc: 'ja4prezz@gmail.com', body: '''Build complete 

Landmark Technologies''', cc: 'ja4prezz@gmail.com', from: '', replyTo: '', subject: 'Build failed', to: 'ja4prezz@gmail.com'
    }
    success {
    mail bcc: 'ja4prezz@gmail.com', body: '''Build complete 

Landmark Technologies''', cc: 'ja4prezz@gmail.com', from: '', replyTo: '', subject: 'Build succeed', to: 'ja4prezz@gmail.com'
    }
  }  
  }
