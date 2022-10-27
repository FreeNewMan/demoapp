node("linux"){
    stage("Git checkout"){
        git credentialsId: '15711219-9cd1-4659-9137-48c98ec36275', branch: 'main', url: 'git@github.com:FreeNewMan/demoapp.git'
        def cur_tag = sh(returnStdout: true, script: "git tag --sort version:refname | tail -1").trim()
    }
    stage("Sample define secret_check"){
        secret_check=true
    }

   def app

    stage('Build image') {
        app = docker.build("lutovp/demoapp")
    }

    stage('Test image') {
        app.inside {
            sh 'echo Hello'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push(cur_tag)
        }
    }    



}
