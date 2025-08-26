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
                sh "pwd"
            }
        }
    }
    post {
        cleanup {
            cleanWs()
        }
    }
}