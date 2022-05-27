pipeline {
    agent {
        kubernetes {
            label 'sample-app'
            defaultContainer 'jnlp'
            yamlFile 'k8sPod.yaml'
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
                // git 'http://github.com/tangjoe/...'
                sh 'echo checkout sources here'
            }
        }
        stage('Check tools') {
            parallel {
                stage('Test golang') {
                    steps {
                        container('golang') {
                            sh """
                            go version
                            sleep 36000
                            """
                        }
                    }
                }
                stage('Test maven') {
                    steps {
                        git 'https://github.com/tangjoe/helloworld.git'
                        container('maven') {
                            sh """
                            mvn clean install
                            mvn package
                            """
                        }
                    }
                }
                stage('Test python') {
                    steps {
                        container('python') {
                            sh """
                            python3 --version
                            sleep 36000
                            """
                        }
                    }
                }
            }
        }
    }
}
