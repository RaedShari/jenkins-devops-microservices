pipeline{
	agent any

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage("Checkout"){
			steps {
				sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "Path - $PATH"
				echo "Build Id - $env.BUILD_ID"
			}
		}
		stage("Compile"){
			steps {
				sh "mvn clean compile"
			}
		}
		stage("Test"){
			steps {
				sh "mvn test"
			}
		}
		stage("Integration Test"){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage("Package"){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage("Build Docker Image"){
			steps {
				//sh "docker build -t raedwaili/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("raedwaili/currency-exchange-devops:{$env.BUILD_TAG}")
				}
			}
		}
		stage("Push Docker Image"){
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest')
					}
				}
			}
		}
	}
	post {
		always{
			echo "====++++always++++===="
		}
		success{
			echo "====++++only when successful++++===="
		}
		failure{
			echo "====++++only when failed++++===="
		}
	}
}
