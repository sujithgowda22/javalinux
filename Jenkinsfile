pipeline{
 agent any
 
 stages{
  stage('build'){
   steps{
    sh 'ant -f build.xml -v'
	echo "PipeLine"
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
	
			
