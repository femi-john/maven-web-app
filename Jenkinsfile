node
{
def mavenHome = tool name: "maven3.6.3"
    
    stage("1. git clone")
    {
       git credentialsId: 'GitCredentials', url: 'https://github.com/myLandmakTechnology/maven-web-app'
    }
    
    stage("2. Build")
    {
        sh "${mavenHome}/bin/mvn clean package"

    }
    stage('3. SonarQubeReport')
    {
         sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('4. Nexus')
     {
         sh "${mavenHome}/bin/mvn deploy"
    }
    stage('5. Deploy')
    {
        deploy adapters: [tomcat9(credentialsId: 'Tomcat-Credentials', path: '', url: 'http://54.163.156.108:8888/')], contextPath: null, war: 'target/*war'
    }

    stage('6. Email Notification')
    {

emailext body: '''Hi

Build Status
Landmark Technology
+ 1 437 215 2483''', recipientProviders: [developers()], subject: 'Build status', to: 'legah2000@gmail.com'    
    }
   }
