pipeline {
    agent any
    environment {
        SERVER_CREDENTIALS = credentials('sample-global-credentials') // "Credentials" and "Credentials binding" plugins must be installed to use credentials()
    }
    triggers {
        pollSCM('H/1 * * * *')
    }
    stages {
        stage("test") {
            steps {
                sh "node helloworld.js"
            }
        }
        stage("another") {
            steps {
                // another way to ket credentials locally inside an stage when other stages dont need them
                withCredentials([
                    usernamePassword(credentials: 'sample-global-credentials', usernameVariable: USER, passwordVariable: PASSWORD)
                ]) {
                    echo "username=${USER}, password=${PASSWORD}"
                }
            }
        }
        stage("deploy") {
            steps {
                echo "Deploying with credentials: ${SERVER_CREDENTIALS}"
            }
        }
    }
}
