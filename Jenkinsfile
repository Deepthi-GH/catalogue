pipeline {
    // This is a pre build section
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        COURSE = "Jenkins"
        appVersion = ""
    }
    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    // This is a build section.
    stages {
        stage('Read Version') {
            steps {
                script {
                     def packageJson = readJSON file: 'package.json'
                     appVersion = packageJson.version
                     echo "app version is : ${appVersion}"
                }
                
            }
        }
        stage('Install Dependencies') {
            steps {
                script { 
                     sh """
                        npm install

                     """
                }
             
            }
        }

         stage('Build Image') {
            steps {
                script { 
                     sh """
                        docker build -t kattika:${appVersion} .
                        docker images

                     """
                }
             
            }
        }

        stage('Deploy') {
            //  input {
            //     message "Should we continue?"
            //     ok "Yes, we should."
            //     submitter "alice,bob"
            //     parameters {
            //         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            //     }
            // }
            when {
                expression { "$params.DEPLOY" == "true" }
            }
            steps {
                script {
                    sh """
                        echo "Deploying"
                    """

                }
                
            }
        }

    }

    post {
        always {
            echo 'I will always say hello again!'
            cleanWs()
        }

        success {
            echo 'I will run if success'
        }
       
       failure {
           echo 'I will run if failure'
       }
       aborted {
            echo 'pipeline is aborted'
       }
    }
}