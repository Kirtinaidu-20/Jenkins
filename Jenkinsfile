pipeline {
    agent any
        
    environment{
        deploydir = "/var/lib/tomcat/webapps/"
    }

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

        stage('deploy application to tomcat server')
        {
            steps{
                sh "sudo cp -rvf target/vivekapp.war ${deploydir}"
                sh "sudo systemctl restart tomcat9"
            }
        }
    }
    post {
        success {
            echo 'Deployment successful! Application is live on Tomcat server.'
            mail to: 'kolatarun95@gmail.com',
                subject:'Build success'
                body:'pipeline running successfully' 
        }
        failure {
            echo 'Deployment failed.'
            mail to: 'kolatarun95@gmail.com',
                subject:'Build failed'
                body:'pipeline failed. Check jenkins' 
        }
    }

}