pipeline {
    agent {
        node {
            label ""
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