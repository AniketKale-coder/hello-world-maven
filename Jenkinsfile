pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
         stage('Deploy') {
            steps {
                script {
                    def tomcatBaseUrl = 'http://174.129.249.22:8080'  // Replace with your Tomcat server URL
                    def warFileName = 'hello-world.war'  // Replace with the name of your generated WAR file

                    def deployUrl = "${tomcatBaseUrl}/manager/text/deploy?path=/&war=file:${warFileName}"
                    def auth = 'admin:ani1234'  // Replace with your Tomcat manager username and password

                    sh "curl -T target/${warFileName} --user ${auth} ${deployUrl}"
                }
            }
        }
    }
}
