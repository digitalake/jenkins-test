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
            sh (
            'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"-607571432\", \"text\": \"Jenkins says hi\"}\' https://api.telegram.org/bot5736407974:AAF_mvzzO7jjzaNYgxn2inImUX7Rg0f0VZ4/sendMessage'
            )
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
//    post {
//        always {
//            withCredentials([string(credentialsId: 'TelegramBotToken', variable: 'TOKEN'), string(credentialsId: 'TelegramGroupID', variable: 'CHAT_ID')]) {
//                sh  ("""
//                curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*Job*: ${env.JOB_NAME} *Branch*: ${env.BRANCH_NAME} *Build* ${env.BUILD_NUMBER} *Result* ${currentBuild.currentResult}'
//                """)
//            }
//        }
//    }
}
