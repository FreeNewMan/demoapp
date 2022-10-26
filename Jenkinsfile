node("linux"){
    stage("Git checkout"){
        git credentialsId: 'f7a92abb-51aa-48ea-8b25-b7b36a52f411', url: 'git@github.com:FreeNewMan/demoapp.git'
    }
    stage("Sample define secret_check"){
        secret_check=true
    }
}
