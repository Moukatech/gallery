pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        git 'https://github.com/Moukatech/gallery.git'
      }
    }
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Deploy to Heroku') {
        steps {
            sh 'git push https://git.heroku.com/secret-spire-84057.git'
            }
    }
    stage('Run Test') {
        steps {
            sh 'npm test'
            }
    }
    stage('Send Slack Notification') {
        steps {
            slackSend channel: 'YourFirstName_IP1', color: 'good', message: 'Successfully deployed to Heroku'
        }
    }
     post {
        success {
            emailext attachLog: true,
                body:
                    """
                    <p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p>
                    <p>
                    View console output at
                    "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"
                    </p>
                      <p><i>(Build log is attached.)</i></p>
                    """,
                subject: "Status: 'SUCCESS' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'",
                to: 'lewis.mocha@student.moringaschool.com'
        }
        failure {
            emailext attachLog: true,
                body:
                    """
                    <p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p>
                    <p>
                    View console output at
                    "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"
                    </p>
                      <p><i>(Build log is attached.)</i></p>
                    """,
                subject: "Status: FAILURE -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'",
                to: 'lewis.mocha@student.moringaschool.com'
        }
     }
  }
}
