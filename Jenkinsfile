pipeline {
  agent any
  triggers{
    pollSCM('H/2 * * * *')
  }
  stages {
    stage('Build Application') { 
      steps {
        //sh 'mvn clean install'
        sh 'mvn clean package'

      }  
    }
 	// stage('Test') { 
  //     steps {
  //       echo 'Test Appplication...' 
  //       sh 'mvn test'
  //     }
  //   }
 	
   
	stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypointPlatform')
      }
            
      steps {
        echo 'Deploying only because of code commit...'
        echo 'Deploying to  dev environent....'
              sh 'mvn deploy -DmuleDeploy -Dusername=MiriamB -Dpassword=Usmc1775! -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2'

       //sh 'mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2'
      // sh 'mvn clean package deploy -DmuleDeploy -Dmule.verbose.exception=true -DmuleDeploy.prop.skipMaven=true -Denv=cloudhub -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2'

      }
	  
	}
  }
}