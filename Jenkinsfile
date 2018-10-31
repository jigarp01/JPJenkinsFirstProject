pipeline {
    agent any

    triggers{
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building .... "
                bat 'mvn clean package'
            }
            post {
                success {
                    echo "Now Archiving ... "
                    archiveArtifacts artifacts: '**/target/*.war'

                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy to Staging Started... "
                bat "./JenkinsShell.bat"
            }
        }
    }
}
