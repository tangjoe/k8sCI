pipeline {
    agent {
        kubernetes {
            label 'helloworld'
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
        stage('Mavne clean/install/package') {
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
        stage('Buid image')
            steps {
                container('kaniko') {
                    sh """
                    /kaniko/executor --context `pwd` --destination tangjoe88/helloworld:1.0
                    """
                }
            }
        }
    }
}
