pipeline {
	    agent any
	    stages {
	        stage("Checkout code") {
	            steps {
	                checkout scm
	            }
	        }
	        stage('Build image') {
	            when{
	                anyOf{
	                    expression{env.BRANCH_NAME == 'master'}
	                    expression{env.BRANCH_NAME == 'develop'}
	                }
	            }
	            steps{
	                script {
	                    ms1 = docker.build("fourth-memento-307608/ms1","-f ./cicd/Dockerfile ./ ")
	                }
	                script {
	                    docker.withRegistry('https://eu.gcr.io', 'gcr:gcr-admin-key') {
	                        ms1.push("latest")
	                    }                    
	                }
	            }
	        }
	        stage ('Push container from develop branch to dev cluster') {
	            steps{
	                build job: 'deploy-to-k8s', parameters: [[$class: 'StringParameterValue', name: 'ms-name', value: 'ms1']]
	            }    
	        }
	    }
}
