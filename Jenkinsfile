pipeline{
 agent none
 
  environment {
    MAJOR_VERSION = 1
  }
 
/* options{
  buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
  }*/
 
 stages{
  stage('Unit Test'){
   agent{
	 label 'master'
   }
   steps{
	sh 'ant -f test.xml -v'
	junit 'reports/result.xml'
   }
  }
  
  stage('build'){
   agent{
	 label 'master'
   }
   steps{
    sh 'ant -f build.xml -v'
	echo "PipeLine"
   }	
   post{
    success{
     //archive 'dist/*jar'
     archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true
     }   
    }
  }
  
  stage('deploy'){
   agent{
	 label 'master'
   }
   steps{
	    sh "if ![ -d '/var/www/html/rectangles/all/${env.BRANCH_NAME}' ]; then mkdir /var/www/html/rectangles/all/${env.BRANCH_NAME}; fi"
        sh "cp dist/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}/"
      }
   }   
  

	


 }
}
	
			
