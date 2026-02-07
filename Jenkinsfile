pipeline {
    agent any

    stages {
        stage('Build') {
        steps {
            echo 'Building...'
        }
        }
    }
    // ⭐ Slack Notifications
    post {
        success {
            slackSend(
                channel: '#devops-ensi', 
                color: 'good', 
                message: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
            )
        }
        failure {
            slackSend(
                channel: '#devops-ensi', 
                color: 'danger', 
                message: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
            )
        }
    }

}
