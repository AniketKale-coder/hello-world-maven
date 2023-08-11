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
                    
                    def credentials = credentials('af844fb0-271a-4056-9189-d9d53084e74f')  // Replace 'credential-id' with your actual credential ID
                    def tomcatUsername = credentials.username
                    def tomcatPassword = credentials.password
                    def auth = "${tomcatUsername}:${tomcatPassword}" 
                    
                    echo "${tomcatUsername}:${tomcatPassword}"
                    
                    def tomcatBaseUrl = 'http://174.129.249.22:8080'  
                    def warFileName = 'hello-world.war'  
                  
                    def deployUrl = "${tomcatBaseUrl}/manager/text/deploy?path=/&war=file:${warFileName}"
                    def curlCommand = "curl -T target/${warFileName} --user ${auth} ${deployUrl}"
                    def curlOutput = sh(script: curlCommand, returnStdout: true).trim()

                    echo "curl command output:\n${curlOutput}"
                }
            }
        }
    }
}
