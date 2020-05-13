pipeline{
	agent any

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome:bin:$PATH"
	}
	stages {
		stage("Build"){
			steps {
				sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "Path - $PATH"
				echo "Build Id - $env.BUILD_ID"
			}
		}
		stage("Test"){
			steps {
				echo "Test"
			}
		}
		stage("Integration Test"){
			steps {
				echo "Integration Test"
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
