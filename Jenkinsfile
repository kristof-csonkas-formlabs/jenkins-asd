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
                ).readLines().drop(1).dropRight(1).join(" /PID ") // header, terminating empty line
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