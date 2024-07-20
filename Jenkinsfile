pipeline {
    agent {
        label 'Agent-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        ansiColor('xterm')
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'appversion', defaultValue: '1.0.0', description: 'Who should I say hello to?')

    }
    environment {
        def appversion = ''
        nexusUrl = 'nexus.srikantheswar.online:8081'
    }
    
    stages {
        stage('read the package') { 
            steps {
                sh """
                    echo "app version ${params.appversion}"
                """
                
            }
        }
        stage('init') {
            steps {
                sh """
                cd terraform
                cd terraform init -reconfigure
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                    cd terraform
                    cd terraform plan -var="${appversion}"
                """
            }
        }
        stage('deploy') {
            steps {
                sh """
                 cd terraform
                 cd terraform apply -auto-approve -var="${appversion}"
                """
            }
        }
    }
    post {
        always {
            echo "i will run always"
        }
        success {
            echo "i will run pipeline is success"
        }
        failure {
            echo "i will run pipeline is failure"
        }
    }
}