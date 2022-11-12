pipeline {
	agent any

    tools {nodejs "node"}

	stages {
		stage('First pipeline testing') {
			steps {
                echo "We're in the first pipeline, working as intended."
			}
		}

        stage("OWASP DependencyCheck"){
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
            }
        }

        stage("NodeJS test")
        steps{
            echo "simple test below"
            sh 'npm config ls'
        }
	}

    post {
        success{
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}