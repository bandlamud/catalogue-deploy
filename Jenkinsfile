pipeline {
    agent {
        node {
            label 'AGENT-1'
            
        }
    }
    environment { 
        COURSE = 'jenkins'
        appVersion = " "
        ACC_ID = "022779559954"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
        REGION = "us-east-1"
    }
    options {
        timeout(time: 1, unit: 'HOURS') 
        disableConcurrentBuilds()
    }
     parameters {
        string(name: 'appVersion', description: 'which app version you want to deploy')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'Pick something')

    }

    stages{
        stage('Deploy') {
            steps {
                script {
                    withAWS(region:'us-east-1',credentials:'aws-creds'){
                    sh """
                        aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}-${params.deploy_to}
                    """

                    }
                }
            }
        }
    }
    
    
        
    post { 
        always { 
            echo 'I will always say Hello again!'
            cleanWs()
            }
            success {
                echo 'i will run if success'
            }
            failure {
                echo 'i will run if failure'
            }
            aborted {
                echo 'pipeline is aborted'
            }
        }
    }