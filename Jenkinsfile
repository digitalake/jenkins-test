pipeline {
    agent any
    stages {
       stage(" List env Variables") {
            steps {
                sh "printenv"
            }
        }
       stage('test') {
           steps {
               echo "Starting tests..."
               echo "testing ${env.BUILD_ID} on ${env.JENKINS_URL}"
           }
       }
       stage('build') {
        steps {
            echo "jenkins build id: ${env.BUILD_ID}"
            echo "commit hash: ${env.GIT_COMMIT}"
        }
       }
       stage('Conditional') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo "HOLA from ${env.BRANCH_NAME}"
                    }  else {
                        sh "echo 'you cannot get HOLA when running on ${env.BRANCH_NAME} branch!'"
                    }
                }
            }
        }
    }
    post {
        always {
            withCredentials([string(credentialsId: 'TelegramBotToken', variable: 'TG_TOKEN'), string(credentialsId: 'TelegramGroupID', variable: 'GROUP_ID')]) {
                sh (
                'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"<your-chat-id>\", \"text\": \"Pipeline build finished with success\"}\' https://api.telegram.org/bot<your-tg-token>/sendMessage'
                )
            }
        }
    }
}
