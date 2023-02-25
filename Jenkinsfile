pipeline {
	agent any

	environment {
		mavenHome = tool 'jenkins-maven'

		 // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "nexus-release"
        NEXUS_CREDENTIAL_ID = "nexus-credentials"
	}

	tools {
		jdk 'java-17'
	}

	stages {

		stage('Build'){
			steps {
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
			    bat "mvn jar:jar deploy:deploy"
			}
		}
	}
}
