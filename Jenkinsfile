pipeline {
    agent {
        docker {
            image 'node:7-alpine' 
            args '-p 3000:3000' 
        }
    }
	environment {
        CI = 'true'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
		 stage('Test') {
            steps {
				sh 'chmod -R 777 ./jenkins/scripts/*.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
		stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver-for-development.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
