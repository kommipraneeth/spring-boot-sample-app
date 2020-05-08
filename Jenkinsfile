pipeline {
    agent any
	stages {
		stage('SCM Checkout'){
		    steps{
			    git credentialsId: 'NA', url: 'https://github.com/kommipraneeth/spring-boot-sample-app'
			}
		}

		stage('Compile Package'){
			steps{
			    sh 'mvn clean install -DSkipTests'
			}
        }
    }
}