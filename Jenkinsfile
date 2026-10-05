pipeline {
    agent any

    stages {

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

        stage('Deploy') {
            steps {
                sh 'sudo cp target/vivekapp.war /var/lib/tomcat11/webapps/vivekapp.war'
                sh 'sudo systemctl restart tomcat11'
            }
        }
    }
}