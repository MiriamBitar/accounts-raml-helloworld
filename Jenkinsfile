pipeline {
  agent {label 'master'}
  triggers{
    pollSCM('H/2 * * * *')
  }
  stages {
    stage('Build Application') { 
      steps {

        echo "Current date: $now"
        sh 'sudo apt -y autoremove'
        sh 'sudo apt install ca-certificates'
        sh 'sudo apt update && apt install -y maven'
        sh 'mvn clean install'
      }  
    }
 	stage('Test') { 
      steps {
        echo 'Test Appplication...' 
        sh 'mvn test'
      }
    }
 	
   
	stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypointPlatform')
      }
            
      steps {
        echo 'Deploying only because of code commit...'
        echo 'Deploying to  dev environent....'
        sh 'mvn package deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2'
      }
	  
	}
  }
}