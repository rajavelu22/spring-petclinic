pipeline {
	agent { label 'slave1' }
	
	options { timeout(time: 1, unit: 'HOURS') }
	
	triggers { cron('* * * * *') }

	stages {
		stage('Git Clone') {
			steps {
				git url: 'https://github.com/rajavelu22/spring-petclinic.git', branch: 'main'
			}
		}
		
		stage('Build Package') {
			steps {
				sh '/opt/apache-maven-3.9.9/bin/mvn package'
			}
		}
		
		stage('Run Tests') {
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
