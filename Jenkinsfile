pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'call mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
