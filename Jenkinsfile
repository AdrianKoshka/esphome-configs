node("fedvm") {
    stage("Clone") {
        cleanWs deleteDirs: true
        checkout scmGit(branches: [[name: '*/main']], extensions: [cloneOption(depth: 1, noTags: false, reference: '', shallow: true)], userRemoteConfigs: [[credentialsId: 'git-clone-key', url: 'git@github.com:AdrianKoshka/esphome-configs.git']])
            
    }
    stage("Validate") {
        sh("podman run --rm -v '${env.WORKSPACE}':/config ghcr.io/esphome/esphome config airgradient-one.yaml")
    }
    stage("Build") {
        sh("podman run --rm -v '${env.WORKSPACE}':/config ghcr.io/esphome/esphome compile airgradient-one.yaml")
    }
}