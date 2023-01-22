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
            sh ""curl -X POST -H "Content-Type: application/json" -d "{\"chat_id\": \"-607571432\", \"text\": \"CI: new version was uploaded, see: https://preview.startup.com\"}" https://api.telegram.org/bot5736407974:AAF_mvzzO7jjzaNYgxn2inImUX7Rg0f0VZ4/sendMessage""
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
}
