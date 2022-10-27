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
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("lutovp/demoapp")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'curl localhost'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            //app.push("${env.BUILD_NUMBER}")
            app.push(cur_tag)
        }
    }    



}
