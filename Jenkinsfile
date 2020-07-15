def emailNotification (String developerEmail, String emailSubject='', String emailBody='', String attachments = '')
{
    emailext attachLog: true, attachmentsPattern: "$attachments", body: "$emailBody", subject: "$emailSubject", to: "$developerEmail"
}

node 
{
   stage ('Conformation to start the Job')
   {
      input message: '', parameters: [booleanParam(defaultValue: false, description: 'Check the if box you wish to create infrastructure for the job first', name: 'start_job')]
   }
   stage('Clone src code') 
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
   stage('Clone attendance_deploy_role and mysql_role')
   {
      try
      {
         echo "Cloning attendance_deploy_role and mysql_role"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Update attendance_deploy_role')
   {
      try
      {
         echo "Updating attendance_deploy_role"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Update Inventory')
   {
      try
      {
         echo "Updating Inventory"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Check If host Present')
   {
      try
      {
         echo "Checking If host Present'"
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Check If Application Present in Host')
   {
      try
      {
         echo "Checking If application Present in Host'"
         //if present take backup
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
         //restore backup
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('start attendence CD job')
   {
      echo "Build attendence CD Job"
      build job: '/cd_multibranch/prod_attendance', propagate: false, wait: false
   }

}
