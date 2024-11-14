pipeline {
	agent any
	
	options { timeout(time: 1, unit: 'HOURS') }
	
	triggers { cron('0 * * * *') }
         parameters {
                choice(name: 'GOAL', choices: ['clean', 'clean package', 'clean install'], description: 'GOALS FOR MAVEN')
         }
	stages {
		stage('Git Clone') {
			steps {
				git url: 'https://github.com/rajavelu22/spring-petclinic.git', branch: 'main'
			}
		}
		
		stage('Build Package') {
			steps {
				sh "/opt/apache-maven-3.9.9/bin/mvn ${params.GOAL}"
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
