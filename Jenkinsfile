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
	 label 'apache'
   }
   steps{
	sh 'ant -f test.xml -v'
	junit 'reports/result.xml'
   }
  }
  
  stage('build'){
   agent{
	 label 'apache'
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
	 label 'apache'
   }
   steps{
	    sh "pwd"
	    sh " if [ ! -d '/var/www/html/rectangles/all/${env.BRANCH_NAME}' ]; then mkdir /var/www/html/rectangles/all/${env.BRANCH_NAME}; fi"
        sh "cp dist/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}/"
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
  
  
 }
}
	
			
