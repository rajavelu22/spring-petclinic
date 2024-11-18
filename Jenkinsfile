pipeline {
	agent { label 'slave' } 
	stages {
		stage('Git Clone') {
			steps {
				git url: 'https://github.com/rajavelu22/spring-petclinic.git', branch: 'main'
			}
		}
		
		stage('Build Package and sonarQube analysis') {
			steps {
				
                                 withSonarQubeEnv('My SonarQube Server') {
                                sh "mvn clean package sonar:sonar -e -X"
              }
			}
		}
		
		stage('Archiving the reports for xml') {
			steps {
				junit testResults: 'target/surefire-reports/*.xml'
			}
		}
	}
	
	post {
		success {
			echo "Pipeline completed successfully"
		}
		
		failure {
			echo "Pipeline failed"
		}
	}
}
