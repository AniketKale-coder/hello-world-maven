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
                    
                    // def credentials = credentials('db2b9465-2df1-4930-b9a9-d49ab049031d')  // Replace 'credential-id' with your actual credential ID
                    // def tomcatUsername = credentials.username
                    // def tomcatPassword = credentials.password
                    def auth = "tomcatsc:ani1234 

                    def tomcatBaseUrl = 'http://174.129.249.22:8080'  
                    def warFileName = 'hello-world.war'  
                  
                    def deployUrl = "${tomcatBaseUrl}/manager/text/deploy?path=/&war=file:${warFileName}"
                    def curlCommand = "curl -T target/hello-world.war --user ${auth} ${deployUrl}"
                    def curlOutput = sh(script: curlCommand, returnStdout: true).trim()

                    echo "curl command output:\n${curlOutput}"
                }
            }
        }
    }
}
