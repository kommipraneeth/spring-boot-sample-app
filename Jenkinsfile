pipeline {
    agent any
    tools {
        maven 'Maven'
        java 'JDK'
    }
	stages {
		stage('SCM Checkout'){
		    steps{
			    git credentialsId: 'NA', url: 'https://github.com/kommipraneeth/spring-boot-sample-app'
			}
		}

		stage('Compile Package'){
			steps{
			    sh 'mvn install -DskipTests'
			}
        }
    }
}