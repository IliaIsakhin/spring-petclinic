pipeline {
	agent any
	tools {
                maven 'maven-3.5.0'
                jdk 'java-1.8'
                git 'Default'
        }
	stages {
                stage('Sonar is running') {
                        steps {
                                withSonarQubeEnv('sonarqube-6.7.5') {
                                        bat 'mvn sonar:sonar'
                                }
                        }
                }

                stage('Tests is running') {
                        steps {
                                bat 'mvn clean test -Dmaven.test.failure.ignore=false'
                        }
                }

                stage('Build is running') {
                        steps {
                                bat 'mvn package -Dmaven.test.skip=true'
                        }
                }
	}
	
	post {
                always {
                        junit '**/surefire-reports/*.xml'
                }
                success {
                    emailext (
                        subject: "Success: Job ${JOB_NAME} ${BUILD_NUMBER}", 
                        replyTo: "", 
                        body: """SUCCESSFUL: Job '${JOB_NAME} [${BUILD_NUMBER}]':</p> <p>Check console output at "<a href="${BUILD_URL}">${JOB_NAME} [${BUILD_NUMBER}]</a>"</p>""",
                        to: 'ilia_isakhin@epam.com'
                    )
                }
                failure {
                   emailext (
                        subject: "Failure: Job ${JOB_NAME} ${BUILD_NUMBER}", 
                        replyTo: "", 
                        body: """Failure: Job '${JOB_NAME} [${BUILD_NUMBER}]':</p> <p>Check console output at "<a href="${BUILD_URL}">${JOB_NAME} [${BUILD_NUMBER}]</a>"</p>""",
                        to: 'ilia_isakhin@epam.com'
                    )
                }
        } 
}
	
