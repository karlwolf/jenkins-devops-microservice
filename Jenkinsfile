pipeline {
	agent any
	//agent {	docker { image 'node:14.4' } }
	stages{
		stage('Build'){
			steps{
				//sh 'node --version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "$env.BUILD_ID"
				echo "$env.BUILD_TAG"
			}
		}
		stage('Test'){
			steps{
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}
		}
	} 
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run when success'
		}
		failure {
			echo 'I run when failure'
		}		
	}
}
