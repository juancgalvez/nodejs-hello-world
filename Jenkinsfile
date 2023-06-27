pipeline {
    agent any
    triggers {
        pollSCM('H/1 * * * *')
    }
    stages {
        stage("test") {
            steps {
                sh "node helloworld.js"
            }
        }
    }
}
