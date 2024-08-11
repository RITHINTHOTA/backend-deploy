pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm') 
    }
    environment {
        def appVersion = ''
        nexusUrl = 'nexus.rithinexpense.online:8081'
    }
    stages {
        stage('print the version'){
            steps{
                script{
                    echo "Application version: ${params.appVersion}"
                }
            }
        }
        stage('init'){
            steps{
                sh """
                cd terraform
                terraform init
                """
            }
        }
        stage('plan'){
            steps{
                sh """
                cd terraform
                terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }
        // stage('Deploy'){
        //     steps{
        //         sh """
        //         cd terraform
        //         terraform apply -auto-approve
        //         """
        //     }
        // }
    }   
    post{
        always {
          deleteDir()
        }
        success{
             echo "It will run when the pipeline is success"
        }
        failure {
             echo "It will run when the pipeline is failure" 
        }
    }