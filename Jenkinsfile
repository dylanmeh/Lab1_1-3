pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: ubuntu
    command:
    - sleep
    args:
    - infinity
'''
            defaultContainer 'shell'
        }
    }
    stages {
        stage('Main') {
            steps {
                sh 'hostname'
            }
        }
    }
    post {
        always {
            emailext (
              subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
              body: """SUCCESSFUL: Job '${JOB_NAME} [${BUILD_NUMBER}]':
              Check console output at ${BUILD_URL}""",
              to: 'ted.fenn@concanon.com'
            )
        }
    }
}