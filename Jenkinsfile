pipeline {
    // agent { docker { image 'python:3.5.1' } }
    agent any 
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            slackSend channel: '#jenkins',
                  color: 'good',
                  message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
        }
        failure {
            echo 'This will run only if failed'
            mail to: 'jeroenifumi@gmail.com',
                  subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                  body: "Something is wrong with ${env.BUILD_URL}"
            //slackSend channel: '#jenkins',
            //      color: 'good',
            //      message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
