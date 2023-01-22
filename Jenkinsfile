pipeline {
   agent any
   stages {
       stage('hello-stage') {
           steps {
               echo "hello world"
               echo "${env.BUILD_ID} on ${env.JENKINS_URL}"
           }
       }
   }
}
