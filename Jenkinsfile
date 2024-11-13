pipeline {
	
	agent { label 'slave1' }
	
	options { timeout(time: 1, unit: 'HOURS') }
	
	 triggers { ('* * * * *') }

	stages {
		stage('Git Clone'){
			
			steps {
			
				git url: 'https://github.com/rajavelu22/spring-petclinic.git', branch :'main'
		
			}
		}
	stage('Git Package'){

                        steps {

				sh 'mvn clean package'				
                        }
                }

	stage('Git Package'){

                        steps {

				junit testResults : 'target/surefire-reports/*.xml'	
                        }
                }

        }
	post {

			success {
				echo "successull"
			}

			unsuccessful {
				echo "unsuccessfull"
			}


	}
}
