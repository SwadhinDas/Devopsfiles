node
{
def mavenHome = tool name: "maven3.6.3" 

   stage('Checkoutcode')
   {
   git branch: 'development', credentialsId: '5fad9887-5c61-4670-8f49-b743f856ac7b', url: 'https://github.com/SwadhinDas/maven-web-application.git'
   }
   
   stage('CreateBuild')
   {
   sh "${mavenHome}/bin/mvn clean package"
   }
   stage('Executesonarqubereport')
   {
   sh "${mavenHome}/bin/mvn sonar:sonar"
   }
   stage('uploadintonexus')
   {
   sh "${mavenHome}/bin/mvn deploy"
   }
  stage('Deploytheapplicationintotomcatserver')
  {
  sshagent(['TomcatserverCredentials'])
  {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.198.179:/opt/apache-tomcat-9.0.38/webapps/"
  }
  }
  stage('EmailNotification')
  {
  mail bcc: '', body: '''Build is Over.....

Regards
Swadhin Das''', cc: '', from: '', replyTo: '', subject: 'Build Status', to: 'swadhindas100@gmail.com'
  }
  
}
