node("linux"){
    stage("Git checkout"){
        git credentialsId: '695f967b-89da-415f-913d-a18d744b53da', url: 'git@github.com:FreeNewMan/demoapp.git'
    }
    stage("Sample define secret_check"){
        secret_check=true
    }
}
