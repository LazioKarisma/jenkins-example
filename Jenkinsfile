pipeline {
    agent any
  
  	tools { 
        maven 'maven-3.8.1'
        jdk 'jdk8' 
    }

    stages {
        stage('Build') {
            steps {
                // To run Maven on a Windows agent, use
                 bat 'mvn clean test'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
					echo 'success'
					
			archiveArtifacts artifacts: 'target/surefire-reports/com.techprimers.testing.FizzBuzzTest.txt', onlyIfSuccessful: true
								
			emailext attachLog: true, attachmentsPattern: 'target/surefire-reports/com.techprimers.testing.FizzBuzzTest.txt',
			subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          subject: 'Test Jenkins Pipeline', to: 'lazio_karisma@manulife.com'
                }
            }
        }
    }
}
