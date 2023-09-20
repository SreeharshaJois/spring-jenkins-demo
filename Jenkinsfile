pipeline {
	agent any

	environment {
		mavenHome = tool 'jenkins-maven'
	}

	tools {
		jdk 'java-17'
		maven 'jenkins-maven'
	}

	stages {

		stage('Build'){
			steps {
				sh "mvn clean install -DskipTests"
			}
		}
		 stage('SonarQube analysis') {
      			steps {
        			script {
          			// requires SonarQube Scanner 2.8+
          			scannerHome = tool 'SonarQube Scanner 5.0.1'
       			 }
        		withSonarQubeEnv('SonarQube Scanner') {
         			 sh "${scannerHome}/bin/sonar-scanner"
        		}
      }
    }
		stage('Test'){
			steps{
				sh "mvn test"
			}
		}

		stage('Deploy') {
			steps {
			    sh "mvn jar:jar deploy:deploy"
			}
		}
	}
}
