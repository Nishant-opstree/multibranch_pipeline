def emailNotification (String developerEmail, String emailSubject='', String emailBody='', String attachments = '')
{
    emailext attachLog: true, attachmentsPattern: "$attachments", body: "$emailBody", subject: "$emailSubject", to: "$developerEmail"
}

node 
{
   stage ('Conformation to start the Job')
   {
      input message: '', parameters: [booleanParam(defaultValue: false, description: 'Confirm if you wish to start the job', name: 'start_job')]
   }
   stage('Cloning src code') 
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
   stage('Cloning terraform code') 
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
   stage('Create Test Infrastructure')
   {
      try
      {
         echo "Creating test infrastructure for attendance and mysql"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Download attendance_deploy_role and mysql_role')
   {
      try
      {
         echo "attendance_deploy_role and mysql_role"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Deploy Attendance app to test Infrastructure and Configure Mysql Creds')
   {
      try
      {
         echo "Deploying Attendance and mysql code"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Test Atttendance Application')
   {
      try
      {
         echo "Testing code"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('start attendence CD job')
   {
      echo "Build attendence CD Job"
      build job: 'attendance_prod', propagate: false, wait: false
   }

}
