pipeline {

	agent any
	//agent { docker {image 'maven:3.6.3'} }
	environment {
		mavenHome = tool "myMaven"
		dockerHome = tool "myDocker"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
	} 
	// post {
	// 	always {
	// 		echo 'Im awesome. I run always'
	// 	}
	// 	success {
	// 		echo 'I run when you are successfull'
	// 	}
	// 	failure {
	// 		echo 'I run when you fail'
	// 	}
	// }
	
}