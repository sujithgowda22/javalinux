pipeline{
 agent none
 
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
	sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar    /var/www/html/rectangles/all"
   }   
  }
  
  stage("Test on Debian") {
      agent {
        docker 'openjdk:8u121-jre'
      }
      steps {
        sh "wget http://ec2-54-245-132-213.us-west-2.compute.amazonaws.com/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar 3 4"
      }
    }
	
  stage('Promote to Green') {
      agent {
        label 'master'
      }
      when {
        branch 'master'
      }
      steps {
        sh "cp /var/www/html/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/green/rectangle_${env.MAJOR_VERSION}.${devBuild}.jar"
      }
  }

 }
}
	
			
