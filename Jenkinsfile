node('nodes')
{
def mavenHome = tool name : "maven3.6.3"
stage('GettingtheCodeFromGithub')
{
git branch: 'development', credentialsId: '4cb05b65-6111-4373-8acd-2dda4364344d', url: 'https://github.com/SwadhinDas/maven-web-application.git'
}
stage('CreateBuild')
{
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('Sonarqubereport')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('UploadArtifactIntoNexus')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployToTomact')
{
sshagent(['TomcatserverCredentialsforpipeline']) 
{
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.127.164.181:/opt/apache-tomcat-9.0.45/webapps/"
}
}
*/
stage('EmailNotification')
{
mail bcc: '', body: 'Build is Over...', cc: '', from: '', replyTo: '', subject: 'BUILD STATUS', to: 'swadhindas100@gmail.com'
}
}
