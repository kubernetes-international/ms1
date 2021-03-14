node{
    checkout scm
    stage('Build image') {
       app = docker.build("test/test")
    }
    stage('Push image') {
        docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}