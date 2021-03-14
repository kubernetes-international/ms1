node{
    checkout scm
    if (env.BRANCH_NAME ==~ /(develop|master|main)/) {
        
        stage('Build image ') {
            app = docker.build("fourth-memento-307608/test")
        }
        
        if (env.BRANCH_NAME ==~ /(develop)/ )  {
            stage('Push image develop') {
                docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                    app.push("latest")
                }
            }
        }

        if (env.BRANCH_NAME ==~ /(master)/ )  {
            stage('Push image master') {
                docker.withRegistry('https://eu.gcr.io', 'gcr:google-container-registry') {
                    app.push("${env.BUILD_NUMBER}")
                }
            }
        }
        
    }
}