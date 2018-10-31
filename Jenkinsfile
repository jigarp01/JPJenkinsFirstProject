pipeline {
    agent any

    parameters {
        string(name: 'tomcat_dev', defaultValue: '35.153.140.177', description: 'My Staging server')
    }

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
