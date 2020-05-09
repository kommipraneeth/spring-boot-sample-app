pipeline {
    agent any
    tools {
        maven 'apache-maven-3.6.3'
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