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
                echo "Now Archiving ... "
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy to Staging Started... "
                bat "pscp -i C:/Users/jigarp/Documents/MyProjects/JenkinsSelfLearning/MyEC2NewKP.pem **/target/*.war ec2-user@$(params.tomcat_dev):/var/lib/tomcat8/webapps"
            }
        }
    }
}
