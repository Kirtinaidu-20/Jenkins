pipeline {
    agent {
        label 'slavenode'
    
    }

    /*environment{
        deploydir = "/var/lib/tomcat/webapps/"
    }*/

    triggers{
        githubPush()
    }

    stages {

        stage('checkout'){
            steps{
                git 'https://github.com/Kirtinaidu-20/Jenkins'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Checking code coverage') {
            steps {
                sh 'mvn clean verify'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful! Application is live on Tomcat11.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }

}