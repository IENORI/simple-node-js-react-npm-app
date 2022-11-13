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

        stage("Testing some random nodejs, cloning"){
            steps{
                git 'https://github.com/gustavoapolinario/node-todo-frontend'
            }
        }
        stage("installing node dependencies"){
            steps{
                sh 'npm install'
            }
        }
        stage("running node test"){
            steps{
                sh "npm test"
                echo "test completed"
            }
        }
	}

    post {
        success{
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}