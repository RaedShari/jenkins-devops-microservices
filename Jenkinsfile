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
				sh "mvn failsafetest:integration-test failsafe:verify"
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
