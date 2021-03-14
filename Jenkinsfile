node{
    checkout scm
    stage('Build image ') {
        when { anyOf { branch 'develop'; branch 'master' } }
        app = docker.build("fourth-memento-307608/test")
    }
    stage('Push image develop') {
        when {  branch 'develop' }
        docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    stage('Push image master') {
        when {  branch 'develop' }
        docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}