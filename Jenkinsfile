pipeline {
    agent any
    tools {
        maven 'Maven 3.6.3'
        jdk 'jdk8'
    }
	stages {
		stage('SCM Checkout'){
		    steps{
			    git credentialsId: 'NA', url: 'https://github.com/kommipraneeth/spring-boot-sample-app'
			}
		}

		stage('Compile Package'){
			steps{
			    sh 'maven install -DskipTests'
			}
        }
    }
}