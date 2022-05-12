node
{
    def mavenHome = tool name: "maven-3.8.5"
    
    echo "The Node name is:  ${env.NODE_NAME} "
    echo "The Job name is:  ${env.JOB_NAME} "
    echo "The Build number is: ${env.BUILD_NUMBER} "
    echo "The Workspace path is: ${env.WORKSPACE} "
    echo "The Jenkins Home is: ${env.JENKINS_HOME} "
    
    stage('CheckoutCode')
    {
        git branch: 'development', credentialsId: '268a20bf-7452-44a0-82fd-0ac81f58c01c', url: 'https://github.com/My-Learning-Project-Organization/maven-web-application.git'
    }
    
    stage('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('UploadtoNexusRepo')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
   /*
    stage('DeploytoTomcatServer')
    {
        sshagent(['']) {
        sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war tomcat@172.26.245.146:/mnt/e/My_Workspace/tomcat/apache-tomcat-9.0.62/webapps/"
        }
    }
    */
    
    stage('MailNotificationToUser')
    {
        emailext body: '''Hi,
        Build Finished........!!!
        
        Regards,
        Prashant Rajput''', subject: 'Build Over..!!', to: 'prashantrajput@gmail.com'
    }
    
}
