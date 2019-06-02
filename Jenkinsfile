node{
    
   def mvnHome = tool name: 'maven3.6.1', type: 'maven'
   
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3'))])
    
   stage('CheckoutCode'){
       
       git branch: 'development', credentialsId: '5cce856d-5e92-438d-b284-5dd624bb1305', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
   }
   
   stage('Build'){
       
     sh  "${mvnHome}/bin/mvn clean package"
   }
   
   stage('ExecuteSonarQubeReport'){
       
      sh  "${mvnHome}/bin/mvn sonar:sonar"  
      
   }
   
   stage('UploadBuildintoNexus'){
       
      sh  "${mvnHome}/bin/mvn deploy"  
      
   }
   
   stage('DeployAppIntoTomcat'){
       
      sshagent(['tomcatServer']) {
           sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.32.110:/opt/apache-tomcat-9.0.20/webapps/maven-web-application.war"
      } 
   }
   
   stage('SendEmailNotification'){
       
       mail bcc: '', body: '''Build is over.

Regards,
Mithun Technologies,
9980923226.
''', cc: 'ajay.aak@gmail.com, reddygs24@gmail.com', from: '', replyTo: '', subject: 'Build is over', to: 'devopstrainingblr@gmail.com'
   }
    
}
