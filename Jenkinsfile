pipeline {
	
	// Why agent is 'any'?
    agent any
	
    stages {
        stage('Build: Gradle Clean - Test - Build') {
            steps {
                echo 'BUILD: Start'
				
				//buildall task logic
				//sh './gradlew clean test'
				//sh './gradlew clean integrationTest'
				//sh ./gradlew clean assemble
				
				// Running up Gradle buil along with JUnit
				sh './gradlew clean build'
				
				echo 'BUILD: End'
            }
        }
        stage('Deploy: PCF Web - Servie') {
			when {
				branch 'master'
			}
            steps {
                echo 'BUILD: Start'
				
				// PCF push with Gradle-PCF plugin
                withCredentials([[
					
					// Configuration
					$class          : 'UsernamePasswordMultiBinding',
					credentialsId   : 'PCF-CTS-CREDENTIAL',
					usernameVariable: 'USERNAME',
					passwordVariable: 'PASSWORD']]) {

					// CF Command
                    sh '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    sh '/usr/local/bin/cf push'
                }
                echo 'BUILD: End'
            }
        }
        stage('Publish: Nexsus Artifactory') {
            steps {
                echo 'PUBLISH: Start'

				// PCF push with Gradle-PCF plugin
				withCredentials([[
					
					// Configuration
					$class          : 'UsernamePasswordMultiBinding',
					credentialsId   : 'NEXUS-LOGIN',
					usernameVariable: 'USERNAME',
					passwordVariable: 'PASSWORD']]) {

					// CF Command
					sh './gradlew publish'
				}
				
                echo 'PUBLISH: End'
            }
        }
    }
}