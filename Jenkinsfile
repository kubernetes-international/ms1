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
                    ms1 = docker.build("fourth-memento-307608/test","-f ./cicd/Dockerfile ./ ")
                }
                script {
                    docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                        ms1.push("latest")
                    }                    
                }
            }
        }
        stage('Push develop branch to GCR') {
            when {
                branch 'develop'
            }
            steps{
                script {
                    docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                        ms1.push("latest")
                    }                    
                }
            }
        }
        stage('Push master branch to GCR') {
            when {
                branch 'master'
            }
            steps{
                script {
                    docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                        ms1.push("${env.BUILD_NUMBER}")
                    }                    
                }
            }
        }
    }
}
