node
{
   def terraform_code ='https://github.com/Nishant-opstree/terraform.git'
   def test_application = "test_attendance"
   stage('Clone terraform code')
   {
   	try
      {
         echo "Cloning code for attendence from remote repo"
         git credentialsId: 'nishant_github_account', url: """${terraform_code}"""
         sh """
         if [ ! -z ${test_application} ] 
         then
            mv ./test_application_main/${test_application}.tf main.tf
         fi
         """
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Initialize Terraform')
   {
      try
      {
         echo "Initializing Terraform"
         sh 'terraform init'
      }
      catch (err)
      {
         //restore backup
         
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Plan Terraform')
   {
      try
      {
         echo "Planning Terraform"
         sh 'terraform plan'
      }
      catch (err)
      {
         //restore backup
         
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Confirmation to apply the code')
   {
      try
      {
         echo "Confirmation"
         input message: '', parameters: [booleanParam(defaultValue: false, description: 'Do you want to build the code?', name: 'confirmation')]
      }
      catch (err)
      {
         //restore backup
         
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Apply Code')
   {
      try
      {
         echo "Testing code"
         sh 'terraform apply -auto-approve'
      }
      catch (err)
      {
         //restore backup
         
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
}