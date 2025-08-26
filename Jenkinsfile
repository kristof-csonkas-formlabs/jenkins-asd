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
                def escapedWorkspace = WORKSPACE.replaceAll("\\", "\\\\")
            }
            sh "wmic process where 'ExecutablePath=\"${escapedWorkspace}\"' get ProcessId"
        }
    }
}