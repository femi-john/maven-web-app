node
{
    def mavenHome = tool name: "maven"
stage('1. CodeClone')
{
    git credentialsId: 'Git-Credentials', url: 'https://github.com/john-femi/maven-web-app.git'
}
stage('2. Build')
{
    sh "${mavenHome}/bin/mvn package"
}
stage('3. CodeQuality')
{
    sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('4. UploadNexus')
{
    sh "${mavenHome}/bin/mvn deploy"
}
stage('5. Approval')
{
    echo "Approved. Ready for deployment"
}
stage('6. TomcatDeployment')
{
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credential', path: '', url: 'http://3.96.54.134:8888')], contextPath: null, war: 'target/*war'
}
stage('7. Notification' )
{
    emailextrecipients([developers()])
}
    
}
