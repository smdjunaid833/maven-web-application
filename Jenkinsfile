pipeline
{
    
 agent any
 
 tools
 {
    maven "maven3.8.7"
 }
 
  stages
  {
      
      stage('checkout')
      {
          steps
          {
              git credentialsId: 'github-creds', url: 'https://github.com/smdjunaid833/maven-web-application.git'
          }
      }
      
      stage('build')
      {
          steps
          {
              sh "mvn clean package"
          }
      }
      
     stage('sonar-report') 
     {
         steps
         {
             sh "mvn clean sonar:sonar"
         }
     }
      
      stage('nexus-repo')
      {
          steps
          {
              sh "mvn clean deploy"
          }
      }
      
      stage('deploy-tomcat')
      {
          steps
          {
             deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://52.198.57.141:8080/')], contextPath: null, war: '**/maven-web-application.war'
          }
      }
      
  }
}
