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
				sh 'mvn clean package'
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
