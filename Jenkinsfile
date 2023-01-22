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
       stage('Conditional') {
        if (env.BRANCH_NAME == 'main') {
            echo 'Hello from main branch'
        } else {
            sh "echo 'Hello from ${env.BRANCH_NAME} branch!'"
        }
    }
   }
}
