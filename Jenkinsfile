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
                def pids = sh(
                    script: "wmic process where 'ExecutablePath LIKE \"${WORKSPACE.replace("\\", "\\\\")}%\"' get ProcessId",
                    returnStdout: true
                ).replace("\\r", "").split("\\n").dropRight(1)
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