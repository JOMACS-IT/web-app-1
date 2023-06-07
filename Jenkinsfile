pipeline{
    agent any
    tools{
        maven "maven3.9.0"
        
    }
    stages{
        stage ("1. Git clone from repo"){
            steps{
                sh ("echo start git clone from repo")
                git branch: 'main', credentialsId: 'tomcatcred', url: 'https://github.com/JOMACS-IT/web-app-1.git'
                sh "echo end of git clone"
                
            }
        }
        stage("2. Build from Maven"){
        steps{
          sh "echo start building from Maven"
          sh "mvn clean package"
          sh "echo end of build"
        }  
      }
      stage("3. Code quality scan with sonar"){
        steps{
          sh "echo start code quality scan"
          sh "mvn sonar:sonar"
          sh "echo end of build"
        }  
      }
      stage ("4. send slack notification to developers"){
          steps{
              sh "echo start sending notification"
             slackSend channel: '#ci-cd', message: 'successfully built artifact' 
          }
      }
      stage ("5. Store built artifact in nexus"){
          steps{
              sh "echo start deployment to nexus"
              sh "mvn deploy"
              sh "echo end of deployment"
          }
      }
      stage ("6. Deploy to Tomcat server in UAT"){
          steps{
              sh "echo start deployment"
deploy adapters: [tomcat9(credentialsId: 'tomcatcred', path: '', url: 'http://16.170.201.165:8080/')], contextPath: null, war: 'target/*.war'
             sh "echo end of deployment"
          }
          
    /*      
      }
      stage("7. Approval from P.M"){
          steps{
              sh "echo approval require from PM"
              timeout(time:3, unit:'DAYS'){
                  input message: "Approval from PM required"
              }
          }
      }
      stage ("8. Deployment to Prod Env"){
          steps{
              sh "echo start deployment to prod env"
              deploy adapters: [tomcat9(credentialsId: 'tomcatcred', path: '', url: 'http://16.170.201.165:8080/')], contextPath: null, war: 'target/*.war'
              sh "echo end of deployment"
          }
      }
      stage ("9. Send email to developers"){
          steps{
              sh "echo start sending mails"
              emailext body: 'Artifact has successfully been deployed', subject: 'successful deployment', to: 'successfulprince302@gmail.com'
          }
      }
      */
    }
     
}
        
    
