pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building stage!'
                sh 'make build'
            }
        }
        stage('Unit tests') {
            steps {
                sh 'make test-unit'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }
        stage('Unit test API') {
            steps {
                sh 'make test-api'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }
        stage('Unit test E2E') {
            steps {
                sh 'make test-e2e'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }
    }
    post {
        always {
            junit 'results/*_result.xml'
            cleanWs()
        }
        success {  
             echo 'Exito Pipeline --->' 
         }  
         failure {  
             echo 'ERROR Pipeline---->'  
             mail to: 'alexynaru@gmail.com', body: "<b>Pipeline - ERROR</b><br>Proyecto: ${env.JOB_NAME} <br>N&uacute;mero compilaci&oacute;n: ${env.BUILD_NUMBER} <br> URL de compilaci&oacute;n: ${env.BUILD_URL}", charset: 'UTF-8', mimeType: 'text/html', subject: "ERROR CI: Nombre del proyecto -> ${env.JOB_NAME}";  
         }  
    }
}
