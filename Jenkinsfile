pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'BUILD: Start'
				sh './gradlew clean build'
				echo 'BUILD: End'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}