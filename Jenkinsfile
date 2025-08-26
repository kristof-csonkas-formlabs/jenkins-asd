def killProcesses(dir) {

}

pipeline {
    agent {
        node {
            label ""
            customWorkspace "workspace/repo-" + UUID.randomUUID().toString()
        }
    }
    stages {
        stage("Start") {
            steps {
                cleanWs()
                sh "pwd"
            }
        }
    }
    post {
        cleanup {
            sh "wmic process ExecutablePath=\"$WORKSPACE\" get ProcessId"
        }
    }
}