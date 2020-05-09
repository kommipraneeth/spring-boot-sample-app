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

		//stage('Dependancy') {
        //   steps {
        //       sh 'mkdir -p build/owasp'
        //       dependencycheck additionalArguments: '--project plastinforme --scan ./ --data /home/jenkins/security/owasp-nvd/ --out build/owasp/dependency-check-report.xml --format XML', odcInstallation: 'OWASP'
        //       dependencyCheckPublisher failedTotalCritical: 1, failedTotalHigh: 3, failedTotalLow: 10, pattern: 'build/owasp/dependency-check-report.xml', unstableTotalCritical: 1, unstableTotalHigh: 2, unstableTotalLow: 5
        //       archiveArtifacts(allowEmptyArchive: true,artifacts: '**/dependency-check-report.*',onlyIfSuccessful: true)
        //   }
        //}

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

        stage('Integration tests') {
                    // Run integration test
           steps {
                 //def mvnHome = tool 'Maven 3.5.2'
                 // just to trigger the integration test without unit testing
                 sh 'mvn verify -Dunit-tests.skip=true'
                 // cucumber reports collection
                 cucumber buildStatus: null, fileIncludePattern: '**/cucumber.json', jsonReportDirectory: 'target', sortingMethod: 'ALPHABETICAL'
           }
        }

        stage('Sonar Analysis') {
            // Run the sonar scan
            steps {
               withSonarQubeEnv('Sonar') {
                   sh 'mvn verify sonar:sonar -Dintegration-tests.skip=true -Dmaven.test.failure.ignore=true'
               }
            }
        }

        // waiting for sonar results based into the configured web hook in Sonar server which push the status back to jenkins
        stage('Sonar Scan Quality Gate Check') {
             steps {
                 timeout(time: 5, unit: 'MINUTES') {
                     retry(3) {
                         script {
                             def qg = waitForQualityGate()
                             if (qg.status != 'OK') {
                                error "Pipeline aborted due to quality gate failure: ${qg.status}"
                             }
                         }
                     }
                 }
             }
        }

        stage('Integration tests') {
                    // Run integration test
           steps {
                 //def mvnHome = tool 'Maven 3.5.2'
                 // just to trigger the integration test without unit testing
                 sh 'mvn verify -Dunit-tests.skip=true'
                 // cucumber reports collection
                 cucumber buildStatus: null, fileIncludePattern: '**/cucumber.json', jsonReportDirectory: 'target', sortingMethod: 'ALPHABETICAL'
           }
        }
    }
}