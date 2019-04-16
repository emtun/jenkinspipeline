pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '3.14.1.188', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.191.164.169', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "scp -i \\C:\\Users\\Emre\\AmazonAWS\\tomcat-demo.pem \\C:\\Program Files (x86)\\Jenkins\\workspace\\FullyAutomated\\webapp\\target\\*.war ec2-user@${params.tomcat_dev}:\\var\\lib\\tomcat7\\webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "scp -i \\C:\\Users\\Emre\\AmazonAWS\\tomcat-demo.pem \\C:\\Program Files (x86)\\Jenkins\\workspace\\FullyAutomated\\webapp\\target\\*.war ec2-user@${params.tomcat_prod}:\\var\\lib\\tomcat7\\webapps"
                    }
                }
            }
        }
    }
}
