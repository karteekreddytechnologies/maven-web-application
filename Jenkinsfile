node('node1')
{
    def mavenhome = tool name: "maven3.8.2"
    stage('checkoutcode')
    {
        git branch: 'development', credentialsId: '1909533c-dd48-4e40-af0e-aaf3fede7fc8', url: 'https://github.com/karteekreddytechnologies/maven-web-application.git'
    }
    stage('Build')
    {
        sh "${mavenhome}/bin/mvn clean package"
    }
    stage('execution of sonarqube report')
    {
        sh "${mavenhome}/bin/mvn sonar:sonar"
    }
    stage('upload artifact in nexus')
    {
        sh "${mavenhome}/bin/mvn deploy"
    }
    stage('deploy app in to tomcat')
    {
        sshagent(['06124995-2e57-472a-83e5-3c937cb9e17d']) 
        {
        sh "scp -o stricthostkeychecking=no target/maven-web-application.war ec2-user@65.0.185.38:/opt/apache-tomcat-9.0.53/webapps/"
        }
        
    }
    /*
    stage('send email notification')
    {
        mail bcc: '', body: '''build over 



regrads,
karteek.''', cc: '', from: '', replyTo: '', subject: 'build over', to: 'karteekreddy453@gmail.com'
    }
    */
}
