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
            echo "commit author: ${env.GIT_AUTHOR_NAME}"
            echo "commiter email: ${env.GIT_COMMITTER_EMAIL}"
            telegramSend 'Hello World'
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
