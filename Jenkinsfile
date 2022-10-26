node("linux"){
    stage("Git checkout"){
        git credentialsId: '15711219-9cd1-4659-9137-48c98ec36275', branch: 'main', url: 'git@github.com:FreeNewMan/demoapp.git'
    }
    stage("Sample define secret_check"){
        secret_check=true
    }
}
