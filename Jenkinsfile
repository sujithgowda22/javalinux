pipeline{
 agent{
	 label 'master'
 }
 
/* options{
  buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
  }*/
 
 stages{
  stage('Unit Test'){
   steps{
	sh 'ant -f test.xml -v'
	junit 'reports/result.xml'
   }
  }
  stage('build'){
   steps{
    sh 'ant -f build.xml -v'
	echo "PipeLine"
   }		
  }
  stage('deploy'){
   steps{
	sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar    /var/www/html/rectangles/all
   }   
  }
 }
 post{
  always{
   //archive 'dist/*jar'
   archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true
  }
 }
}
	
			
