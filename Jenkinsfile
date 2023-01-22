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
   }
}
