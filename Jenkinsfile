pipeline {
    agent {
        node {
            customWorkspace "src/other-repo"
        }
    }
    stages {
        stage("Start") {
            steps {
                sh "pwd"
            }
        }
    }
}