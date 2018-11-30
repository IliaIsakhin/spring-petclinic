node {
	stage('Build') {
		echo "${M2_HOME}"
		sh "mvn install"
	}
	stage('Sonar') {
		steps {
			echo 'Running sonar....'
		}
	}
	stage('Test') {
		steps {
			echo 'Testing..'
		}
	}
}

