pipeline {
    agent any
	stages {
		stage('SCM Checkout'){
			git credentialsId: 'NA', url: 'https://github.com/kommipraneeth/spring-boot-sample-app'
			}

		stage('Compile Package'){
			sh 'mvn clean install -DSkipTests'
			}
		}
	}