# jenkins-test
test repo for using jenkins for the first time

### Tasks
To-do:
  - Setup Jenkins on server.
  - Create Multibranch pipeline and connect it with the Gitlab/Github project repository with the Jenkinsfile
  - Jenkinsfile should have several stages: build, tests, notification (telegram bot, etc.)
  - [Optional] Use branch conditions, vars, etc
  - [Optional] Create script for automated Jenkins setup (with user, plugins).
  
### Creating simple multibranch Pipeline with two branches: Dev + Main

In this repo you can find the Jenkinsfile for running simple tasks.

Lets go throurh the code:

#### Declaring pipeline agent and stages section

Code snippet:
```
pipeline {
    agent any
    stages {
    ...
    }
```

#### Stage List env Variables

I decided to print all the variables from ${YOUR_JENKINS_HOST}/env-vars.html 

Code snippet:
```
stage(" List env Variables") {
            steps {
                sh "printenv"
            }
        }
```
#### Stage test

Runs some achos with Jenkins predefined variables

Code snippet:
```
stage('test') {
           steps {
               echo "Starting tests..."
               echo "testing ${env.BUILD_ID} on ${env.JENKINS_URL}"
           }
       }

```

#### Stage build 

Prints some variables

Code snippet:
```
stage('build') {
        steps {
            echo "jenkins build id: ${env.BUILD_ID}"
            echo "commit hash: ${env.GIT_COMMIT}"
        }
       }
```

### Stage Conditional 

In this stage the scripts executes the seperated command for __main__ nd __non-main__ branches using if "condition" syntax 

Code snippet:
```
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
```

### Telegram Notification

Uses curl to telegram api to send a message about successful executing

Code snippet:
```
post {
        always {
            withCredentials([string(credentialsId: 'TelegramBotToken', variable: 'TG_TOKEN'), string(credentialsId: 'TelegramGroupID', variable: 'GROUP_ID')]) {
                sh (
                'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"${GROUP_ID}\", \"text\": \"Pipeline build finished with success\"}\' https://api.telegram.org/bot${TG_TOKEN}/sendMessage'
                )
            }
        }
    }

