pipeline {
   agent any
   stages {
       stage('test') {
           steps {
               echo "hello world"
               echo "${env.BUILD_ID} on ${env.JENKINS_URL}"
           }
       }
       stage('build') {
        steps {
            echo "jenkins is building something"
            echo "build ended"
        }
       }
       stage('deploy') {
        steps {
            echo "deploying..."
        }
       }
       stage('Hello') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo 'hello from main'
                    }  else {
                        sh "echo 'you cannot get hello from ${env.BRANCH_NAME} branch!'"
                    }
                    }
            }
       }
   }
}
