pipeline {
   agent any
tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_HOME'
		git 'GIT'
    }
     stages {
	 	  
      stage('checkout') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/sushmab123/parking_backend.git'
            
            }

             }
			 
			 stage('Analysis') {
         steps {
            
            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean verify"

            }

             }
			  stage('Quality gates') {
         steps {
            
            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true sonar:sonar"

            }

             }
			 
			  stage('Deploy') {
         steps {
            
            // upload artifacts to Nexus.
            sh "mvn -Dmaven.test.failure.ignore=true clean deploy"

            }

             }
			 stage('Release') {
         steps {
            // run the jar file
            sh 'export BUILD_ID=PK'
			sh 'cp $WORKSPACE/src/main/resources/application.properties /opt/parking/'
			//sh '$JAVA_HOME/bin/java -version'
			//sh 'printenv'
			//sh "nohup java -jar $WORKSPACE/target/parking-0.0.1-SNAPSHOT.jar -spring.config.location=file:/opt/parking/application.properties&"
            sh 'export JENKINS_NODE_COOKIE=PK;nohup java -jar $WORKSPACE/target/parking-0.0.1-SNAPSHOT.jar -spring.config.location=file:/opt/parking/application.properties &'
            }

             }
   }
}
