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
                pids = sh(
                    script: "wmic process where 'ExecutablePath LIKE \"${WORKSPACE.replace("\\", "\\\\")}%\"' get ProcessId",
                    returnStdout: true
                ).readLines().drop(1) // header
                if (!pids.isEmpty()) {
                    sh(
                        script: "taskkill /F /T /PID ${pids.join(" /PID ")}"
                    )
                }
            }
        }
    }
}