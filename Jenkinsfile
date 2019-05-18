pipeline {
	agent docker 'node'
	stages {
		stage('Build') {
			steps{
				sh './gradlew clean build'
			}
		}
		stage('Archive Dependencies List') {
			steps{
				sh './gradlew listDependencies'
				archiveArtifacts artifacts: 'buils/reports/dependencies.csv', fingerprint: true
			}
		}
	}
}