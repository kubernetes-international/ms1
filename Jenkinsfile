node{
    checkout scm
    stage('Build image') {
       app = docker.build("fourth-memento-307608/test")
    }
    stage('Push image') {
        docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}