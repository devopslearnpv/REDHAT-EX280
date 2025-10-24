pipeline {
    agent any
 
    stages {
        stage('Failing Step') {
            steps {
                // Intentional failure to test email
                sh 'exit 1'
            }
        }
 
        stage('Another Step') {
            steps {
                echo 'This step will be skipped due to failure above'
            }
        }
    }
 
    post {
        always {
            echo 'Pipeline finished'
        }
 
        success {
            echo 'Pipeline succeeded'
        }
 
        failure {
            emailext(
                subject: "🚨 Jenkins Job '${env.JOB_NAME}' (#${env.BUILD_NUMBER}) Failed!",
                body: """
<p>Hi Team,</p>
<p>The build failed. Check the logs here:</p>
<p><a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html',
                to: 'devopslearnpv@gmail.com'
            )
        }
    }
}