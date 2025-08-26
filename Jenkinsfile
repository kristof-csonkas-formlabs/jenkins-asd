def killProcesses(dir) {

}

pipeline {
    agent {
        node {
            label "windows"
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
            script {
                @NonCPS
                def getPids() {
                    return sh(
                        script: "wmic process where 'ExecutablePath LIKE \"${WORKSPACE.replace("\\", "\\\\")}%\"' get ProcessId",
                        returnStdout: true
                    )
                        .replace("\\r", "")
                        .split("\\n")
                        .findResults {
                            !it.isEmpty()
                        }
                }
                def pids = getPids()
                echo(pids.isEmpty().toString())
                echo(pids)
                if (!pids.isEmpty()) {
                    bat(
                        script: "taskkill /F /T /PID ${pids}"
                    )
                }
            }
        }
    }
}