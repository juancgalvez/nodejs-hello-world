pipeline {
    agent any
    environment {
        SERVER_CREDENTIALS = credentials('sample-global-credentials') // "Credentials" and "Credentials binding" plugins must be installed to use credentials()
    }
    parameters {
        string(name: 'PRODUCT_NAME', defaultValue: 'Test Product', description: 'This is te product name')
        choice(name: 'VERSION', choices: ['2.5.1', '2.6.1', '2.7.1'], description: 'Define what versionj of the product must be built')
        booleanParam(name: 'executeAnotherStage', defaultValue: true, description: 'Boolean value indicating if another Stage gets executed')
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
        stage("deploy") {
            steps {
                echo "Deploying version ${params.VERSION} with credentials: ${SERVER_CREDENTIALS}"
            }
        }
        stage("another") {
            when {
                expression {
                    params.executeAnotherStage
                }
            }
            steps {
                // another way to ket credentials locally inside an stage when other stages dont need them
                withCredentials([
                    usernamePassword(credentialsId: 'sample-global-credentials', usernameVariable: 'USER', passwordVariable: 'PWD')
                ]) {
                    echo "username=${USER}, password=${PWD}"
                }
            }
        }
    }
}
