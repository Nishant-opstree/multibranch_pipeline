def emailNotification (String developerEmail, String emailSubject='', String emailBody='', String attachments = '')
{
   emailext attachLog: true, attachmentsPattern: "$attachments", body: "$emailBody", subject: "$emailSubject", to: "$developerEmail"
}

node 
{
   cleanWs()
   //def configFilePath = input message: 'Enter Configration Path', parameters: [string(defaultValue: '/home/ubuntu/confFile.properties', description: '', name: 'configFilePath', trim: true)]
   //def props = readProperties  file: """${configFilePath}"""
   def create_infra = input message: '', parameters: [booleanParam(defaultValue: false, description: 'Check the if box you wish to create infrastructure for the job first', name: 'create_infra')]
   def src_code ='https://github.com/Nishant-opstree/ot-microservices.git'
   def role_repo = 'https://github.com/Nishant-opstree/roles.git'
   if ( """${create_infra}""" == true)
   {
        stage ('Confirmation to start the Job')
        {
            echo """${create_infra}"""
            //build job: '/infra_multibranch/arc_test', propagate: false, wait: false
        }

   }
   stage('Clone src code')
   {
   	try
      {
         echo "Cloning code for attendence from remote repo"
         git credentialsId: 'nishant_github_account', url: """${src_code}"""
         sh """ mkdir attendance_src
         mv -f attendance/* attendance_src/"""
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
         git branch: 'attendance', credentialsId: 'nishant_github_account', url: """${role_repo}"""
         sh """
            mkdir -p attendence_deploy_role/files/attendance
            mv -f attendance_src/* attendence_deploy_role/files/attendance/"""
          
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
         sh '''
         mysql_ip=$(python dynamic-inventory.py mysql)
         sed -i "/host:/s/mysql/$mysql_ip/" attendence_deploy_role/files/attendance/config.yaml
         '''
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
        def host_tag     = "attendance"
        def key_path = "~/.jenkins/ec2-linux-public-01.pem"
        def service_name = "attendance"
        echo "Checking If application Present in Host'"
        sh script:""" bash backup_script.sh ${host_tag} ${key_path} ${service_name}"""
      }
      catch (err)
      {
         emailNotification ( props['DEVELOPEREMAIL'], 'The code Was Not able to get cloned', 'Build-URL: "${BUILD_URL}"' )
         //slackNotification ( props['SLACKCHANNELDEVELOPER'], 'The cloning of project was not successful Build-URL: "${BUILD_URL}" ')
         sh "exit 1"
      }
   }
   stage('Deploy Attendance app to Production Infrastructure and Configure Mysql Creds')
   {
      try
      {
         echo "Deploying Attendance and mysql code"
         def key_path = "~/.jenkins/ec2-linux-public-01.pem"
         sh """
         key_path=${key_path}
         bash create_inventory.sh attendance ${key_path}
         ansible-playbook -i inventory deploy_attendance.yml
         rm inventory
         if [ ${create_infra} == true ]
         then
            bash create_inventory.sh mysql ${key_path}
            ansible-playbook -i inventory deploy_mysql.yml
            rm inventory
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
}
