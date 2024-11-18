pipeline {
	agent 
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
                                sh "/opt/apache-maven-3.9.9/bin/mvn clean package sonar:sonar"
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
