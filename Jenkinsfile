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
  }
  
 }
}
	
			
