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

		/*stage('Dependancy') {
           steps {
               sh 'mkdir -p build/owasp'
               dependencycheck additionalArguments: '--project plastinforme --scan ./ --data /home/jenkins/security/owasp-nvd/ --out build/owasp/dependency-check-report.xml --format XML', odcInstallation: 'OWASP'
               dependencyCheckPublisher failedTotalCritical: 1, failedTotalHigh: 3, failedTotalLow: 10, pattern: 'build/owasp/dependency-check-report.xml', unstableTotalCritical: 1, unstableTotalHigh: 2, unstableTotalLow: 5
               archiveArtifacts(allowEmptyArchive: true,artifacts: '**/dependency-check-report.*',onlyIfSuccessful: true)
           }
        }*/

		stage('Compile Package'){
		   steps{
		       sh 'mvn install -DskipTests'
               step([$class: 'JacocoPublisher',
                    execPattern: 'target/*.exec',
                    classPattern: 'target/classes',
                    sourcePattern: 'src/main/java',
                    exclusionPattern: 'src/test*'
               ])
		   }
        }
    }
}