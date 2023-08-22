pipeline {
    agent {
        label 'WS'
    }
    environment {
        ENV_URL         = "pipeline.google.com"                  // Pipeline variable
        SSHCRED         = credentials('SSH_CRED') 
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    // triggers { pollSCM('*/1 * * * *') }

    stages {
        stage('Parallel Stages') {
            parallel {
                stage('In Parallel 1') {
                        steps {
                            echo "In Parallel 1"
                            sh "sleep 1"
                            sh "hostname"
                        }
                    }
                stage('In Parallel 2') {
                        steps {
                            echo "In Parallel 2"
                            sleep 1
                    }
                }
                stage('In Parallel 3') {
                        steps {
                            echo "In Parallel 3"
                            sleep 1
                    }
                }
            }
        }
        stage('Stage One') {
            steps {    
                    sh '''
                        echo DevOps Training
                        echo AWS Training
                        echo Batch54
                        echo Name of the URL is ${ENV_URL}
                        sleep 10
                        env

                    '''
            }
        }

        stage('Stage TWO') {
            environment {
                ENV_URL = "stage.google.com"                  // Stage  variab
            }

            // input {
            //     message "Should we continue?"
            //     ok "Yes, we should."
            //     submitter "alice,bob"
            //     parameters {
            //         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            //     }
            // }

            steps {                 
                echo  "This is stage two"
                sleep 13
            }
        }

        stage('Stage THREE') {
            when {  
                anyOf {
                    branch 'dev' 
                    changeset "**/*.js"
                }
            }
            steps {                 
                sh ''' 
                echo "This is stage three"
                echo "Name of the URL is ${ENV_URL}"
                echo -e "\\e[31m Hai"
                sleep 1

                ''' 
            }
        }

        stage('Stage FOUR') {
            steps {                 
                sh ''' 
                echo "This is stage Four"
                echo "Name of the URL is ${ENV_URL}"
                echo -e "\\e[31m Welcome"
                sleep 1

                ''' 
            }
        }
    }

    post { 
        always { 
            cleanWs()
        }
    }
}

// Examples of scripted pipeline

// node {
//     stage('Example') {
//         if (env.BRANCH_NAME == 'master') {
//             echo 'I only execute on the master branch'
           
//         } else {
//             echo 'I execute elsewhere'
//              sh "env"
//         }
//     }
// }