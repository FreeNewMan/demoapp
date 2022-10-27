node("linux"){
    def cur_tag 
    def app

    stage("Git checkout"){
        git credentialsId: '15711219-9cd1-4659-9137-48c98ec36275', branch: 'main', url: 'git@github.com:FreeNewMan/demoapp.git'
        script {
          cur_tag=sh(returnStdout: true, script: "git tag ").trim()
        }
        println ${cur_tag}
    }
    stage("Sample define secret_check"){
        secret_check=true
    }

  

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
            app.push("${cur_tag}")
        }
    }    



}
