pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'JDK'
        git 'Git'
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