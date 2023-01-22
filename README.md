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

Branches screenshot:

![Знімок екрана_20230123_000655](https://user-images.githubusercontent.com/109740456/213942880-94b23803-f6a4-43b3-bf2c-477fe443e30c.png)

Dev:

![Знімок екрана_20230123_000451](https://user-images.githubusercontent.com/109740456/213942928-ee25d546-a5f8-4e46-9616-51be07a3c1bd.png)

Main:

![Знімок екрана_20230123_000438](https://user-images.githubusercontent.com/109740456/213942978-34c8ae5f-954d-4b78-bf82-0857a55c5d89.png)



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

Result for main:

![Знімок екрана_20230123_000248](https://user-images.githubusercontent.com/109740456/213943007-487e065b-c179-4c0b-bd0c-23eb2e0282c9.png)

Result for dev:

![Знімок екрана_20230123_000225](https://user-images.githubusercontent.com/109740456/213943024-385bd67d-1fc6-4622-a4e5-1fd5523cd3d7.png)


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
```

Execution result:

![Знімок екрана_20230123_001257](https://user-images.githubusercontent.com/109740456/213943095-e5ec36c9-b982-448a-8a0b-ceac3beb7567.png)

Telegram notification:

![Знімок екрана_20230123_001436](https://user-images.githubusercontent.com/109740456/213943183-659ca2b3-0c71-409e-bc19-9426002c6062.png)

