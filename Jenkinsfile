pipeline {
	agent any

	environment {
		mavenHome = tool 'jenkins-maven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"

		registryCredentials = "nexus"
        registry = "http://localhost:8081/"
        dockerImage = ''

		 // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "127.0.0.1:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "nexus-release"
	}

	stages {

		stage('Build'){
			steps{
			    bat "java --version"
				bat "mvn clean install -DskipTests"
			}
		}

		stage('Test'){
			steps{
				bat "mvn test"
			}
		}

		stage('Deploy') {
			steps{
				bat "mvn deploy"
			}
		}
	}
}
