pipeline {
    agent any //directive
    
    stages {
        stage ("checkout") {
            steps {
                git branch:'main', url: 'https://github.com/moxquito/course3-jenkins-gs-spring-petclinic'
            }
        }
        
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        
        stage("capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'    
            }
            
        }
    }
    
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to: 'always@nowhere.com',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"

            
        }
    }

}
