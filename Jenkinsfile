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
    }
     
}
   
