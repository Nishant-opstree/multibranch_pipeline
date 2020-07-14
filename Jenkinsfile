def emailNotification (String developerEmail, String emailSubject='', String emailBody='', String attachments = '')
{
    emailext attachLog: true, attachmentsPattern: "$attachments", body: "$emailBody", subject: "$emailSubject", to: "$developerEmail"
}

node 
{
   stage('Cloning stage') 
   {
   	try
      {
         echo "Cloning code for attendence from remote repo"
         git credentialsId: 'nishant_github_account', url: 'https://github.com/Nishant-opstree/ot-microservices.git'
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
}
