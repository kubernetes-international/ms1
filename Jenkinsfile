node{
    checkout scm
    stage('Build image ') {
        if (env.BRANCH_NAME ==~ /(develop|master|main)/) {
            app = docker.build("fourth-memento-307608/test")
        }

    }
    stage('Push image develop') {
        if (env.BRANCH_NAME ==~ develop)  {
            docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                app.push("latest")
            }
        }
    }
    stage('Push image master') {
        if (env.BRANCH_NAME ==~ master)  {
            docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                app.push("${env.BUILD_NUMBER}")
            }
        }
    }
}