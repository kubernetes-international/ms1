pipeline {
	agent any
	stages {
		stage("Checkout code") {
			steps {
				checkout scm
			}
		}


	// Develop chain

		stage('Build image with tag latest for develop branch') {
			when{
				expression{env.GIT_BRANCH == 'origin/develop'}
			}
			steps{
				script {
					ms1 = docker.build("fourth-memento-307608/ms1","-f ./cicd/Dockerfile ./ ")
				}
			}
		}

		stage('Push image with tag latest for develop branch') {
			when{
				expression{env.GIT_BRANCH == 'origin/develop'}
			}
			steps{
				script {
					docker.withRegistry('https://eu.gcr.io', 'gcr:gcr-admin-key') {
						ms1.push("latest")
					}                    
				}
			}
		}

		stage ('Deploy image on dev cluster') {
			when{
				expression{env.GIT_BRANCH == 'origin/develop'}
			}
			steps{
				build job: 'deploy-to-k8s'
			}    
		}
	}
}
