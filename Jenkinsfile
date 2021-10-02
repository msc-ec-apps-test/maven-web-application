node {
    def mavenHome = tool name: "maven3.8.2"
    stage('Checkout'){
        git branch: 'development', credentialsId: '4bf72412-fd6e-42ff-bde7-d79e69737d49', url: 'https://github.com/msc-ec-apps-test/maven-web-application.git'
        
    }
    
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
        
    }
    
    stage('Executingsonarqubereport'){
        
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    
    stage('UploadingArtifactoryinotNexusRepo'){
        
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
    stage('DeployingtoTomcatServer')
    {
        sshagent(['710a7a2c-a7ab-476d-a546-97fb3b1c3515']) 
        {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.31.52:/opt/apache-tomcat-9.0.53/webapps"
        }
    }
/*    
    stage('EmailNotification'){
        mail bcc: 'bhanuchandra217@gmail.com', body: '''Build is Over.

Regards
Banuchandra,
8297354748''', cc: 'bhanuchandra217@gmail.com', from: '', replyTo: '', subject: 'Build is Over.', to: 'bhanuchandra217@gmail.com'
        
    }
*/    
}//closing node
