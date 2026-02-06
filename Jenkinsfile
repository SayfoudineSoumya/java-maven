pipeline {
    agent {
        docker {
        // Image contenant Maven et Git
        image 'my-maven-git:latest'
        // Pour réutiliser le cache Maven local entre builds
        args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('Checkout') {
            steps {
            // clean the directory
            sh "rm -rf *"
            // Checkout the Git repository
            sh "git clone https://github.com/SayfoudineSoumya/java-maven.git"
            }
        }
        stage('Build') {
            steps {
            // Here, we can can run Maven commands
            script {
                def currentDir = pwd()
                echo "Current directory: ${currentDir}"
                // Navigate to the directory containing the Maven project
                dir('java-maven/maven') {
                    // Run Maven commands
                    sh 'mvn clean test package'
                    sh "java -jar target/*.jar"
                }

            }
            }
        }
    }
    // ⭐ Slack Notifications
    post {
        success {
            slackSend(
                channel: '#devops-ensi', 
                color: 'good', 
                message: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
            )
        }
        failure {
            slackSend(
                channel: '#devops-ensi', 
                color: 'danger', 
                message: "❌ FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
            )
        }
        started {
            slackSend(
                channel: '#devops-ensi', 
                color: '#439FE0', 
                message: "🚀 Build STARTED: ${env.JOB_NAME} #${env.BUILD_NUMBER} ${env.BUILD_URL}"
            )
        }
    }

}
