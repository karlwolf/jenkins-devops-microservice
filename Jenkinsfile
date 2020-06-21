pipeline {
	agent any
	//agent {	docker { image 'node:14.4' } }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
			}
		}

		stage('Compile'){
			steps{
				sh 'mvn clean compile'
			}
		}

		stage('Test'){
			steps{
				sh 'mvn test'
			}
		}

		stage('Integration Test'){
			steps{
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}

		stage('Build Docker Image'){
			steps{
				//"docker build -t karlpwolf/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("karlpwolf/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image'){
			steps{
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}				
			}
		}

		stage('Package'){
			steps{
				sh 'mvn package -DskipTests'
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
